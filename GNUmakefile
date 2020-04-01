
#? GNUMAKEFILE_TOPMOST := $(lastword $(MAKEFILE_LIST))

PHONY_TARGETS += all
all ::

GITMODULES_PARTS_SUBDIR ?= .vcshglobal-gitmodules.d
GITMODULES_TARGET_FILE ?= .gitmodules

GITMODULES_PARTS_FULLDIR ?= $(abspath $(GITMODULES_PARTS_SUBDIR))

GITMODULES_SOURCE_FILES := $(sort $(wildcard $(GITMODULES_PARTS_FULLDIR)/[0-9][0-9][-_]*))

# rules {{{
PHONY_TARGETS += clean
clean ::
	@$(RM) -v $(GITMODULES_TARGET_FILE)

$(GITMODULES_TARGET_FILE) : $(GITMODULES_SOURCE_FILES) $(MAKEFILE_LIST)
	@$(info generating $@)awk 1 $(GITMODULES_SOURCE_FILES) > $@ \
		|| { $(RM) -v $@ ; false ; }

all :: $(GITMODULES_TARGET_FILE)
# }}}

# post-rules {{{

.PRECIOUS: $(GITMODULES_SOURCE_FILES)
.PRECIOUS: $(MAKEFILE_LIST)
#? .PRECIOUS: $(GNUMAKEFILE_TOPMOST)
.PHONY: $(PHONY_TARGETS)
# }}}
