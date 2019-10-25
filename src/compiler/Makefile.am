AUTOMAKE_OPTIONS = subdir-objects
AM_YFLAGS = -d -r all
AM_LFLAGS = -d
AM_CXXFLAGS = $(LLVM_CXXFLAGS) -fexceptions
AM_LDFLAGS = $(LLVM_LDFLAGS)

bin_PROGRAMS = blawn

blawn_SOURCES = ast/node.cpp ast/node.hpp compiler/compiler.cpp		\
	compiler/compiler.hpp parser/driver.cpp parser/driver.hpp	\
	parser/main.cpp parser/scanner.hpp				\
	ast_generator/ast_generator.cpp					\
	ast_generator/ast_generator.hpp					\
	ast_generator/node_collector.hpp errors/errors.cpp		\
	errors/errors.hpp utils/utils.cpp utils/utils.hpp		\
	blawn_context/blawn_context.cpp					\
	blawn_context/blawn_context.hpp					\
	global_configuration/global_configuration.cpp			\
	global_configuration/global_configuration.hpp			\
	builtins/builtins.cpp builtins/builtins.hpp			\
	ir_generator/ir_generator.cpp ir_generator/ir_generator.hpp

nodist_blawn_SOURCES = parser/parser.yy parser/lexer.ll

blawn_LDADD = $(LIBCXXFS) $(LLVM_LIBS)

BUILT_SOURCES = parser/parser.cc parser/parser.hh parser/lexer.cc	\
	config-am.h

EXTRA_DIST = parser/parser.yy parser/lexer.ll parser/patch.py	\
	builtins/builtins.ll

CLEANFILES = location.hh position.hh stack.hh parser/parser.output	\
	config-am.h

config-am.h: Makefile
	echo '#define LLVM_LLC "$(LLVM_LLC)"' > $@
	echo '#define PKGLIBDIR "$(pkglibdir)"' >> $@
	echo '#define TMPDIR "/tmp"' >> $@
