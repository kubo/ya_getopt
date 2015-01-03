PROGS = getopt_test getopt_long_test getopt_long_only_test ya_getopt_test ya_getopt_long_test ya_getopt_long_only_test
CFLAGS = -Wall

all: $(PROGS)

check: $(PROGS)
	@for c in 1 2; do \
	  if test $$c -eq 1; then \
	    echo ===== with POSIXLY_CORRECT =====; \
	    export POSIXLY_CORRECT=; \
	  else \
	    echo; \
	    echo ===== without POSIXLY_CORRECT =====; \
	    unset POSIXLY_CORRECT; \
	  fi; \
	  for optstring in "ab:" ":ab:" "ab::" ":ab::" "+ab:" "+:ab:" ":+ab:" "-ab:" "-+ab:" "+-ab:" "-:ab:" ":-ab:"; do \
	    for args in "" \
	                "foo" \
	                "-c" \
	                "-b foo" \
	                "-abfoo" \
	                "-a -b foo bar" \
	                "-b" \
	                "-acb" \
	                "-abc" \
	                "--foo" \
	                "--bar" \
	                "--baz" \
	                "--qux" \
	                "--quux" \
	                "--foo val" \
	                "--bar val" \
	                "--baz val" \
	                "--qux val" \
	                "--quux val" \
	                "--foo=val" \
	                "--bar=val" \
	                "--baz=val" \
	                "--qux=val" \
	                "--quux=val" \
	                "-foo" \
	                "-bar" \
	                "-baz" \
	                "-qux" \
	                "-quux" \
	                "-foo val" \
	                "-bar val" \
	                "-baz val" \
	                "-qux val" \
	                "-quux val" \
	                "-foo=val" \
	                "-bar=val" \
	                "-baz=val" \
	                "-qux=val" \
	                "-quux=val" \
	                "-a foo -b bar" \
	                "-a -- -b bar" \
	                "-a --- -b bar" \
	                "-a foo bar baz -a" \
	                "-a foo bar baz -aa" \
	                "-a foo bar baz -a qux" \
	                "-a foo bar baz -a qux quux" \
	                "-a foo bar baz -a qux quux -a" \
	                "-b arg foo bar baz -b arg" \
	                "-b arg foo bar baz -b arg qux" \
	                "-b arg foo bar baz -b arg qux quux" \
	                "-barg foo bar baz -barg" \
	                "-barg foo bar baz -barg qux" \
	                "-barg foo bar baz -barg qux quux" \
	                "-a foo -b bar -a baz -c qux"; do \
	      echo -n .; \
	      env OPTSTRING=$$optstring ./getopt_test $$args 2> getopt_test.out; \
	      env OPTSTRING=$$optstring ./getopt_long_test $$args 2> getopt_long_test.out; \
	      env OPTSTRING=$$optstring ./getopt_long_only_test $$args 2> getopt_long_only_test.out; \
	      env OPTSTRING=$$optstring ./ya_getopt_test $$args 2> ya_getopt_test.out; \
	      env OPTSTRING=$$optstring ./ya_getopt_long_test $$args 2> ya_getopt_long_test.out; \
	      env OPTSTRING=$$optstring ./ya_getopt_long_only_test $$args 2> ya_getopt_long_only_test.out; \
	      if ! cmp getopt_test.out ya_getopt_test.out >/dev/null; then \
	        echo; \
	        echo OPTSTRING=\'$$optstring\' ARGS=\'$$args\' ... FAILED; \
	        diff -u getopt_test.out ya_getopt_test.out | head -20; \
	        exit 1; \
	      fi; \
	      if ! cmp getopt_long_test.out ya_getopt_long_test.out >/dev/null; then \
	        echo; \
	        echo -n OPTSTRING=\'$$optstring\' ARGS=\'$$args\' ... FAILED; \
	        diff -u getopt_long_test.out ya_getopt_long_test.out | head -20; \
	        exit 1; \
	      fi; \
	      if ! cmp getopt_long_only_test.out ya_getopt_long_only_test.out >/dev/null; then \
	        echo; \
	        echo -n OPTSTRING=\'$$optstring\' ARGS=\'$$args\' ... FAILED; \
	        diff -u getopt_long_only_test.out ya_getopt_long_only_test.out | head -20; \
	        exit 1; \
	      fi; \
	    done; \
	  done; \
	done
	@echo
	@echo PASS ALL

getopt_test: getopt_test.c
	$(CC) $(CFLAGS) -o getopt_test getopt_test.c

getopt_long_test: getopt_long_test.c
	$(CC) $(CFLAGS) -o getopt_long_test getopt_long_test.c

getopt_long_only_test: getopt_long_only_test.c
	$(CC) $(CFLAGS) -o getopt_long_only_test getopt_long_only_test.c

ya_getopt_test: getopt_test.c ../ya_getopt.c ../ya_getopt.h
	$(CC) $(CFLAGS) -o ya_getopt_test -DUSE_YA_GETOPT -I.. getopt_test.c  ../ya_getopt.c

ya_getopt_long_test: getopt_long_test.c ../ya_getopt.c ../ya_getopt.h
	$(CC) $(CFLAGS) -o ya_getopt_long_test -DUSE_YA_GETOPT -I.. getopt_long_test.c  ../ya_getopt.c

ya_getopt_long_only_test: getopt_long_only_test.c ../ya_getopt.c ../ya_getopt.h
	$(CC) $(CFLAGS) -o ya_getopt_long_only_test -DUSE_YA_GETOPT -I.. getopt_long_only_test.c  ../ya_getopt.c

clean:
	$(RM) $(PROGS) getopt_test.out getopt_long_test.out getopt_long_only_test.out ya_getopt_test.out ya_getopt_long_test.out ya_getopt_long_only_test.out
