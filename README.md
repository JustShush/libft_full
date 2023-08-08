# libft_full
This is the normal libft + ft_printf and get_next_line 

## Tutorial on how to use this in your projects
1 - So in the makefile you will need to create a var called `libdir` and give it the name of the lib directory, and then create another variable called `LIBFT` and assign to it the last var + libft.a. Like this:

```sh
libdir = libft
LIBFT = $(libdir)/libft.a
```

2 - Now before the compiling of the main code (NAME) copy and past this code:
```sh
$(LIBFT):
	@make -s -C $(libdir)
```

3 - Now in the compiling part you will need to add `$(LIBFT)` after de sources variable.
*example code*
```sh
$(NAME): $(LIBFT) $(OBJS)
    @$(CC) $(CFLAGS) $(SRCS) $(LIBFT) -o $(NAME)
```

4 - Don't forget to also add the lib to the clean and fclean commands:
```sh
clean:
#  also add here your way to clean your objects
	@make clean --no-print-directory -C $(libdir)

fclean: clean
	@/bin/rm -rf $(NAME) ${OBJ_DIR} $(LIBFT)
```
**Example of complete code of the Makefile:**
```sh
NAME = your_project_name

CC = @cc
CFLAGS = -Wall -Wextra -Werror -g

SRC = main.c \
      utils.c \

libdir = libft
LIBFT = $(libdir)/libft.a

OBJ_DIR = obj
SRCS = $(addprefix src/, $(SRC))
OBJS = $(patsubst src/%, $(OBJ_DIR)/%, $(SRCS:%.c=%.o))

all: $(NAME)

$(LIBFT):
	@make -s -C $(libdir)

$(NAME): $(LIBFT) $(OBJS)
    @$(CC) $(CFLAGS) $(SRCS) $(LIBFT) -o $(NAME)

$(OBJ_DIR)/%.o: $(SRCS)
		@mkdir -p $(OBJ_DIR)
		@$(CC) $(CFLAGS) -o $@ -c $<

clean:
  @/bin/rm -rf $(OBJ_DIR)
	@make clean --no-print-directory -C $(libdir)

fclean: clean
	@/bin/rm -rf $(NAME) ${OBJ_DIR} $(LIBFT)
```
