---
title: file stream
date: 2024-9-6

---

在 C 语言中，文件流是处理文件输入输出的重要概念。以下是一些必须了解的文件流知识点：

### 1. 文件指针
- 使用 `FILE *` 类型的指针来表示文件流。
- 通过 `fopen()` 函数打开文件，返回一个指向 `FILE` 结构的指针。

### 2. 打开和关闭文件
- **打开文件**: 使用 `fopen()` 函数。
  
  ```c
  FILE *fp = fopen("filename.txt", "r"); // "r" 表示只读模式
  //注意：在clion中默认工作目录是cmake-build-debug，这代表使用相对路径时，会到该目录下去寻找文件
  ```
- **关闭文件**: 使用 `fclose()` 函数。
  
  ```c
  fclose(fp);
  ```

### 3. 文件模式
- 常用的文件打开模式：
  - `"r"`: 只读模式
  - `"w"`: 只写模式（如果文件存在会被截断）
  - `"a"`: 追加模式（写入时在文件末尾添加）
  - `"rb"`, `"wb"`, `"ab"`: 二进制模式的读、写和追加

### 4. 文件读写函数
- **读取函数**:
  - `fscanf()`: 从文件中格式化读取数据。
  - `fgets()`: 读取一行字符串。
  - `fread()`: 从文件中读取二进制数据块。

- **写入函数**:
  - `fprintf()`: 向文件中格式化写入数据。
  - `fputs()`: 写入字符串到文件。
  - `fwrite()`: 向文件中写入二进制数据块。

### 5. 文件定位
- 使用 `fseek()`, `ftell()`, `rewind()` 来进行文件指针的定位。
  - `fseek(fp, offset, whence)`: 移动文件指针。
  - `ftell(fp)`: 获取当前文件指针位置。
  - `rewind(fp)`: 将文件指针重置到文件开头。

### 6. 错误处理
- 使用 `ferror()` 检查文件流是否发生错误。
- 使用 `feof()` 检查是否到达文件末尾。

### 7. 标准输入输出文件流
- `stdin`, `stdout`, `stderr`：标准输入、输出和错误流。
- 可以使用 `fprintf(stderr, "Error message\n")` 输出错误信息。

### 8. 文件缓冲
- C 语言的文件流通常是缓冲的，这意味着数据在写入或读取时会先存储在缓冲区中，以提高效率。
- 可以使用 `setbuf()` 或 `setvbuf()` 控制缓冲行为。

### 9. 关闭文件的重要性
- 使用 `fclose()` 来关闭文件，确保所有缓冲数据被写入，并释放相关资源。



### 基础题

1. **文件打开**
   
   - 问题：使用 `fopen()` 打开一个文件时，应如何处理打开失败的情况？请给出示例代码。
   
   
   ```
   FILE *fp = fopen("example.txt", "r");
   if (fp == NULL) {
       perror("Error opening file");
       return 1;
   }
   ```
   
   
   
2. **文件读取**
   - 问题：请编写一段代码，从文本文件中逐行读取内容并打印到标准输出。

   ```
    	FILE *input = fopen("ouput.txt", "r");
       FILE *output = fopen("1.txt", "w");
   
       char buf[1024];
   while (fgets(buf, sizeof(buf), input)!= NULL)
       {
           fputs(buf, output);
       }
   
       fclose(input);
       fclose(output);
   ```
   
   
   
3. **文件写入**
   
   - 问题：如何使用 `fprintf()` 向文件中写入格式化数据？请给出示例。
   
     `fprintf(stderr, "failed: %s"，strerror(errno));`
   
4. **文件关闭**
   
   - 问题：为什么在 C 语言中关闭文件是重要的？如果不关闭文件会发生什么？
     - 它确保所有缓冲的数据被写入到文件中。
     - 释放系统资源，避免内存泄漏。
     - 如果文件未关闭，可能会导致数据丢失或文件损坏。

### 进阶题

5. **文件定位**
   
   - 问题：请解释 `fseek()`、`ftell()` 和 `rewind()` 的功能。给出示例代码，展示如何在文件中定位到特定位置。
   
   ```c
   #include <stdio.h>
   
   int main() {
       FILE *fp = fopen("example.txt", "r");
       if (fp == NULL) return 1;
   
       fseek(fp, 0, SEEK_END); // 定位到文件末尾
       long size = ftell(fp);  // 获取文件大小
       rewind(fp);             // 重置文件指针到开头
   
       printf("File size: %ld bytes\n", size);
       fclose(fp);
       return 0;
   }
   ```
   
   
   
6. **错误处理**
   
   - 问题：如何检测文件操作中的错误？请写出相关的检查代码示例。
   
   ```c
   #include <stdio.h>
   
   int main() {
       FILE *fp = fopen("example.txt", "r");
       if (fp == NULL) {
           perror("Error opening file");
           return 1;
       }
       
       // 进行文件操作
       if (ferror(fp)) {
           perror("Error reading from file");
       }
   
       fclose(fp);
       return 0;
   }
   ```
   
   
   
7. **二进制文件**
   
   - 问题：如何使用 `fread()` 和 `fwrite()` 读取和写入二进制文件？请给出示例代码。
   
   ```c
   #include <stdio.h>
   
   int main() {
       FILE *fp = fopen("data.bin", "wb");
       int numbers[] = {1, 2, 3, 4, 5};
   
       if (fp == NULL) {
           perror("Error opening file");
           return 1;
       }
   
       fwrite(numbers, sizeof(int), 5, fp);
       fclose(fp);
   
       // 读取二进制文件
       fp = fopen("data.bin", "rb");
       int read_numbers[5];
       fread(read_numbers, sizeof(int), 5, fp);
       fclose(fp);
   
       for (int i = 0; i < 5; i++) {
           printf("%d ", read_numbers[i]);
       }
   
       return 0;
   }
   ```
   
   
   
8. **缓冲区**
   
   - 问题：什么是文件的缓冲区？如何使用 `setvbuf()` 来控制缓冲行为？请解释并给出示例。

### 综合题

9. **完整示例**
   - 问题：请编写一个完整的程序，读取一个包含整数的文本文件，计算这些整数的平均值，并将结果写入另一个文件。

   ```c
   #include <stdio.h>
   
   int main() {
       FILE *input = fopen("numbers.txt", "r");
       FILE *output = fopen("result.txt", "w");
       int number, sum = 0, count = 0;
   
       if (input == NULL || output == NULL) {
           perror("Error opening file");
           return 1;
       }
   
       while (fscanf(input, "%d", &number) != EOF) {
           sum += number;
           count++;
       }
   
       if (count > 0) {
           fprintf(output, "Average: %.2f\n", (double)sum / count);
       }
   
       fclose(input);
       fclose(output);
       return 0;
   }
   ```
   
   
   
10. **文件指针**
    - 问题：解释 `ferror()` 和 `feof()` 的区别，并说明它们在文件处理中的作用。
      - `ferror()`: 检查文件流的错误状态，返回非零值表示发生错误。
      - `feof()`: 检查是否到达文件末尾，返回非零值表示已到达末尾。

### 其他

1. 文本文件不过是符合特定编码规则的二进制数据
2. 在window平台要注意区分读文本文件还是二进制文件，因为windows中换行符是\r\n, C语言做了适配读文本数据只会读作\n, 但如果使用rb读就会读入 CR LF，即\r\n

