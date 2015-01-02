all: getopt_test ya_getopt_test

check: getopt_test ya_getopt_test
	@ulimit -t 1; \
	for c in 1 2; do \
	  if test $$c -eq 1; then \
	    echo ===== with POSIXLY_CORRECT =====; \
	    export POSIXLY_CORRECT=; \
	  else \
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
	                "-a foo -b bar" \
	                "-a -- -b bar" \
	                "-a --- -b bar" \
	                "-a foo bar baz -a" \
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
	      echo -n OPTSTRING=\'$$optstring\' ARGS=\'$$args\' ... ; \
	      env OPTSTRING=$$optstring ./getopt_test $$args 2> getopt_test.out; \
	      env OPTSTRING=$$optstring ./ya_getopt_test $$args 2> ya_getopt_test.out; \
	      if cmp getopt_test.out ya_getopt_test.out >/dev/null; then \
	        echo PASS; \
	      else \
	        echo FAILED; \
	        diff -u getopt_test.out ya_getopt_test.out | head -20; \
	        exit 1; \
	      fi; \
	    done; \
	  done; \
	done

getopt_test: getopt_test.c
	$(CC) -o getopt_test getopt_test.c

ya_getopt_test: getopt_test.c ../ya_getopt.c ../ya_getopt.h
	$(CC) -o ya_getopt_test -DUSE_YA_GETOPT -I.. getopt_test.c  ../ya_getopt.c

clean:
	$(RM) getopt_test ya_getopt_test getopt_test.out ya_getopt_test.out
