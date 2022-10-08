# go2make

A tool which generates Makefile logic to mimic what Go does internally.

This used to be part of kubernetes, but no longer.  I didn't want to lose it
entirely, so here is a fork with a bit of history.

## Example:

```
$ ./go2make .
.go2make/by-pkg/github.com/thockin/go2make/_files: /home/thockin/src/go2make
	@mkdir -p $(@D)
	@ls $</*.go | LC_ALL=C sort > $@.tmp
	@if ! cmp -s $@.tmp $@; then \
	    cat $@.tmp > $@; \
	fi
	@rm -f $@.tmp

.go2make/by-pkg/github.com/thockin/go2make/_pkg: .go2make/by-pkg/github.com/thockin/go2make/_files \
  go2make.go
	@mkdir -p $(@D)
	@touch $@

.go2make/by-path//home/thockin/src/go2make/_pkg: .go2make/by-pkg/github.com/thockin/go2make/_pkg
	@mkdir -p $(@D)
	@touch $@
```
