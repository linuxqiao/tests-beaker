#
# Copyright (c) 2019 Red Hat, Inc. All rights reserved.
#
# This copyrighted material is made available to anyone wishing
# to use, modify, copy, or redistribute it subject to the terms
# and conditions of the GNU General Public License version 2.
#
# This program is distributed in the hope that it will be
# useful, but WITHOUT ANY WARRANTY; without even the implied
# warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR
# PURPOSE. See the GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public
# License along with this program; if not, write to the Free
# Software Foundation, Inc., 51 Franklin Street, Fifth Floor,
# Boston, MA 02110-1301, USA.
#

# The toplevel namespace within which the test lives.
TOPLEVEL_NAMESPACE=kernel

# The name of the package under test:
PACKAGE_NAME=

# The path of the test below the package:
RELATIVE_PATH=networking/firewall/netfilter/target

# Version of the Test. Used with make tag.
export TESTVERSION=0.1

# The combined namespace of the test.
export TEST=/$(TOPLEVEL_NAMESPACE)/$(RELATIVE_PATH)

#
# A phony target is one that is not really the name of a file.  It is just a
# name for some commands to be executed when you make an explicit request.
# There are two reasons to use a phony target: to avoid a conflict with a file
# of the same name, and to improve performance.
#
.PHONY: all install download clean

#
# executables to be built should be added here, they will be generated on the
# system under test.
#
BUILT_FILES	= runtest

#
# data files, .c files, scripts anything needed to either compile the test
# and/or run it.
#
FILES	=	$(METADATA) \
		Makefile \
		PURPOSE \
		README.md \
		$(shell ls -1 *.sh)

run: $(FILES) build
	./runtest

build: $(BUILT_FILES)

runtest: runtest.sh
	cp $< $@ && chmod +x $@

clean:
	rm -f *~ *.rpm $(BUILT_FILES)

# Include Common Makefile
# Common Variables
TEST_DIR=/mnt/tests$(TEST)
INSTALL_DIR=$(DEST)$(TEST_DIR)
METADATA=testinfo.desc

# Generate the METADATA file testinfo.desc
$(METADATA): Makefile
	@echo "Owner:        Hangbin Liu <haliu@redhat.com>" > $(METADATA)
	@echo "Name:         $(TEST)" >> $(METADATA)
	@echo "TestVersion:  $(TESTVERSION)" >> $(METADATA)
	@echo "Path:         $(TEST_DIR)" >> $(METADATA)
	@echo "Description:  Basic netfilter tests" >> $(METADATA)
	@echo "Type:         Functional" >> $(METADATA)
	@echo "RunFor:       kernel" >> $(METADATA)
	@echo "Requires:     nmap-ncat socat lksctp-tools" >> $(METADATA)
	@echo "Requires:     tree" >> $(METADATA)
	@echo "repoRequires: networking/common" >> $(METADATA)
	@echo "repoRequires: networking/firewall/000infralib" >> $(METADATA)
	@echo "repoRequires: cki_lib" >> $(METADATA)
	@echo "Priority:     Normal" >> $(METADATA)
	@echo "License:      GPLv2" >> $(METADATA)
	@echo "Confidential: no" >> $(METADATA)
	@echo "Destructive:  no" >> $(METADATA)
