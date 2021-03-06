#
#
#
# Simple Makefile for C/C++ code
# 
# Author: Gustavo Pantuza Coelho Pinto
# Since: 30.05.2014
#
#
#


# Color definition for print purpose
BROWN=\e[0;33m
BLUE=\e[1;34m
END_COLOR=\e[0m


# Source code directory structure
BINDIR := bin
SRCDIR := src
LOGDIR := log
LIBDIR := lib
INCDIR := include


# Source code file extension
SRCEXT := cpp


# Defines the C Compiler
CC := g++


# Defines the language standards for GCC
STD := -std=gnu++11 # use -std=gnu99 for C code. See man gcc for more options

# Protection for stack-smashing attack
STACK := -fstack-protector-all -Wstack-protector

# Specifies to GCC the required warnings
WARNS := -Wall -Wextra -pedantic # -pedantic warns on language standards 

# Flags for compiling
CFLAGS := -O3 $(STD) $(STACK) $(WARNS)

# Debug options 
DEBUG := -g3 -DDEBUG=1

# Dependency libraries
LIBS := -I$(INCDIR) -lm


#
# The binary file name
#
BINARY := tp2


# %.o file names
NAMES := $(notdir $(basename $(wildcard $(SRCDIR)/*.$(SRCEXT))))
OBJECTS :=$(patsubst %,$(LIBDIR)/%.o,$(NAMES))



#
# COMPILATION RULES
#


# Rule for link and generate the binary file
all: $(OBJECTS)
	@echo -en "$(BROWN)LD $(END_COLOR)";
	$(CC) -o $(BINDIR)/$(BINARY) $+ $(DEBUG) $(CFLAGS) $(LIBS) 
	@echo -en "\n--\nBinary file placed at" \
			  "$(BROWN)$(BINDIR)/$(BINARY)$(END_COLOR)\n";


# Rule for object binaries compilation
$(LIBDIR)/%.o: $(SRCDIR)/%.$(SRCEXT)
	@echo -en "$(BROWN)CC $(END_COLOR)";
	$(CC) -c $^ -o $@ $(DEBUG) $(CFLAGS) $(LIBS) 


# Rule for run valgrind tool
valgrind:
	valgrind \
		--track-origins=yes \
		--leak-check=full \
		--leak-resolution=high \
		--log-file=$(LOGDIR)/$@.log \
		$(BINDIR)/$(BINARY)
	@echo -e "\nCheck the log file: $(LOGDIR)/$@.log\n"


# Rule for cleaning the project
clean:
	@rm -rvf $(BINDIR)/*;
	@rm -rvf $(LIBDIR)/*;
	@rm -rvf $(LOGDIR)/*;
