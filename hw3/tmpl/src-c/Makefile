CC = gcc
LEX = flex
YACC = bison
CFLAGS = -Wall -std=gnu11 -g3
LIBS = -lfl -ly
INCLUDE = -Iinclude

SCANNER = scanner
PARSER = parser

COREDIR = lib/core/
CORE := $(shell find $(COREDIR) -name '*.c')

ASTDIR = lib/AST/
AST := $(shell find $(ASTDIR) -name '*.c')

SRC := $(CORE) \
       $(AST)

EXEC = $(PARSER)
OBJS = $(PARSER:=.c) \
       $(SCANNER:=.c) \
       $(SRC)

# Substitution reference
DEPS := $(OBJS:%.c=%.d)
OBJS := $(OBJS:%.c=%.o)

all: $(EXEC)

# Static pattern rule
$(SCANNER).c: %.c: %.l
	$(LEX) -o $@ $<

$(PARSER).c: %.c: %.y
	$(YACC) -o $@ --defines=parser.h -v $<

%.o: %.c
	$(CC) -o $@ $(CFLAGS) $(INCLUDE) -c -MMD $<

$(EXEC): $(OBJS)
	$(CC) -o $@ $^ $(LIBS) $(INCLUDE)

clean:
	$(RM) $(DEPS) $(SCANNER:=.c) $(PARSER:=.c) $(OBJS) $(EXEC)

-include $(DEPS)
