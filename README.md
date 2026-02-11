# get_next_line

A C function that reads a line from a file descriptor, one line at a time.

## Description

`get_next_line` is a function that returns a line read from a file descriptor. This project is part of the 42 School curriculum and demonstrates proficiency in:
- Static variables in C
- File descriptor operations
- Dynamic memory allocation
- Buffer management

## Function Prototype

```c
char *get_next_line(int fd);
```

### Parameters
- `fd`: The file descriptor to read from

### Return Value
- Returns the line read (including the terminating `\n` character if present)
- Returns `NULL` if there is nothing else to read or if an error occurred

## Compilation

Compile the project with your own `main.c` file:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c main.c -o gnl
```

You can change the `BUFFER_SIZE` value to any positive integer:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=1024 get_next_line.c get_next_line_utils.c main.c -o gnl
```

## Usage Example

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main(void)
{
    int fd;
    char *line;

    fd = open("test.txt", O_RDONLY);
    if (fd == -1)
        return (1);
    
    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

## Files

- `get_next_line.c` - Main function implementation
- `get_next_line_utils.c` - Helper functions (ft_strlen, ft_strchr, ft_strdup, ft_strjoin)
- `get_next_line.h` - Header file with function prototypes

## Features

- Reads from file descriptors line by line
- Handles multiple file descriptors (using static variable)
- Configurable buffer size via `BUFFER_SIZE` macro
- Manages memory efficiently with dynamic allocation
- Handles edge cases (empty files, files without newlines, etc.)

## BUFFER_SIZE

The `BUFFER_SIZE` is defined during compilation and determines how many bytes are read from the file descriptor in each `read()` call. The default value is 42 if not specified during compilation.