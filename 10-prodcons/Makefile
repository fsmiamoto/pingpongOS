CC = clang
CFLAGS = -Wall -g3
LD = ld
LDFLAGS = --relocatable
OBJ = ppos.o

TEST_DIR= ./tests
TEST_FLAGS= -g3 # all debug info

all: ppos_core.o ppos_internal.o ppos_ipc.o queue.o 
	$(LD) $(LDFLAGS) $^ -o $(OBJ)

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

$(TEST_DIR)/%.c: all
	$(CC) $(CFLAGS) -DDEBUG $(TEST_FLAGS) $@ $(OBJ) -o $(@:.c=.bin)

build_test: $(TEST_DIR)/*.c

prodcons: all
	$(CC) $(CFLAGS) $(OBJ) prodcons.c -o prodcons

test: $(TEST_DIR)/*.c
	$(TEST_DIR)/bin/run-tests.sh $(TEST_DIR)

clean:
	rm -rf *.o
	rm -rf $(TEST_DIR)/*.bin $(TEST_DIR)/*.output.txt


