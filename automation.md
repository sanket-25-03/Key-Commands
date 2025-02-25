1. file name should be test_*.py or *_test.py

2. function name should be test_*

3. to run all test files
```
pytest or pytest -v 
```

4. To execute the tests from a specific file, use the following syntax −
```
pytest <filename> -v
```

5. To execute the tests containing a string in its name we can use the following syntax −
```
pytest -k <substring> -v
```

6. To run the marked tests, we can use the following syntax −
```
pytest -m <markername> -v
```

7. We can xfail tests using the following marker −
```
@pytest.mark.xfail
```

8. Skipping a test means that the test will not be executed. We can skip tests using the following marker −
```
@pytest.mark.skip
```

9. The syntax to stop the execution of test suite soon after n number of test fails is as follows −
```
pytest --maxfail = <num>
```

10. we can run tests by using the syntax pytest -n <num>
```
pytest -n 3
```
-n <num> runs the tests by using multiple workers, here it is 3.
