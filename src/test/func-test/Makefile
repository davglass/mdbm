
TOPDIR=$(shell realpath $(shell pwd)/../../..)
include $(TOPDIR)/Makefile.base

HEADERS=            \
  TestBase.hh

SOURCES=

COMMON_SOURCES=              \
  CppUnitTestRunnerLocal.cc  \
  TestBase.cc

   
TESTS=                       \
  test_bs                    \
  test_copy_func             \
  test_large_obj             \
  test_lock_func             \
  test_misc_func             \
  test_shake_func            \
  test_single_arch           \
  test_split_func            \
  test_stat                  \
  test_store                 \
  test_window_func           \
  test_replace_func          \
  replace-func-stress-test


MYLIBS =  -L$(TOPDIR)/src/lib/$(OBJDIR) -lmdbm
MYLIBS += -lpthread -lrt -lstdc++ -lcppunit 
LD_EXTRA += $(MYLIBS) -lcppunit $(LOCAL_LDADD)
CXXFLAGS += -I$(TOPDIR)/src/lib

# include locally built libaries in search path...
LD_LIB_PATH=LD_LIBRARY_PATH=$(TOPDIR)/src/lib/$(OBJDIR):$(LD_LIBRARY_PATH)

TESTEXES= $(patsubst %, $(OBJDIR)/%, $(TESTS))

# generate xml test results...
RUN_ARGS= -tall -x $(1).xml 

default-make-target: $(TESTEXES)

# Create the per-test targets.
$(foreach test, $(TESTS), $(eval $(call CppExeTargetRules,$(test),,$(LD_EXTRA))))

test:: $(TESTEXES)
	@echo "RUNNING FUNC TESTS MODE=$(MODE), FAST=$(FAST) !!!!"
	$(foreach test, $(TESTS), make run-$(test) && ) /bin/true

valg:: $(TESTEXES)
	$(foreach test, $(TESTS), make valg-$(test) && ) /bin/true

clean :: clean-objs $(foreach exe, $(TESTS), clean-exe-$(exe))


