## PyTest Commands

### 1. **Run All Tests in the Current Directory**
   ```bash
   pytest
   ```
   **Explanation:** This runs all the test files in the current directory and subdirectories. By default, pytest looks for files starting with `test_` or ending with `_test.py` to execute.

### 2. **Run a Specific Test File**
   ```bash
   pytest path/to/test_file.py
   ```
   **Explanation:** Runs all the test functions in the specified test file. This is useful when you want to focus on the tests in one particular file.

### 3. **Run a Specific Test Class within a File**
   ```bash
   pytest path/to/test_file.py::TestClassName
   ```
   **Explanation:** Runs only the test methods in the specified test class within a file. Use this to isolate and execute all tests within a particular class.

### 4. **Run a Specific Test Function or Method within a Class**
   ```bash
   pytest path/to/test_file.py::TestClassName::test_method_name
   ```
   **Explanation:** This command targets a specific test method within a test class for execution. This is useful when you want to test just one method within a class.

### 5. **Run a Specific Test Function (Standalone Function)**
   ```bash
   pytest path/to/test_file.py::test_function_name
   ```
   **Explanation:** Executes only a single test function from the specified test file. This is useful when you want to run a single test function to troubleshoot or validate functionality.

---

### 6. **Display More Detailed Output (Verbose Mode)**
   ```bash
   pytest -v
   ```
   **Explanation:** Runs all tests but displays more detailed output for each test, showing the name and result of every individual test. Helps in identifying what tests are being run and their outcomes.

### 7. **Display Only Failed Tests with Detailed Information**
   ```bash
   pytest -q --tb=short
   ```
   **Explanation:** Suppresses the regular output, and shows only failed tests along with a shortened traceback. This is useful when debugging failing tests without being overwhelmed by too much information.

### 8. **Show Full Traceback on Failure**
   ```bash
   pytest --tb=long
   ```
   **Explanation:** By default, pytest truncates the error traceback. This command ensures that full traceback details are shown, which can be helpful when debugging complex test failures.

---

### 9. **Run Tests Matching a Pattern**
   ```bash
   pytest -k "pattern"
   ```
   **Explanation:** This command allows you to run tests whose function names match a specific pattern (substring). You can use it to selectively run tests that contain keywords, such as:
   ```bash
   pytest -k "login"
   ```
   This would run all tests with "login" in their names.

### 10. **Stop After the First Failure**
   ```bash
   pytest -x
   ```
   **Explanation:** Stops the test suite execution immediately after the first failure is encountered. This can speed up debugging since you can address the first issue before running further tests.

### 11. **Stop After N Failures**
   ```bash
   pytest --maxfail=3
   ```
   **Explanation:** This command stops the test suite after `N` test failures, where `N` is the number specified. For example, `--maxfail=3` stops the execution after 3 failures, allowing you to limit the number of failures shown.

### 12. **Run Tests in Parallel (Using pytest-xdist Plugin)**
   ```bash
   pytest -n 4
   ```
   **Explanation:** Runs tests in parallel across multiple CPU cores. The number (`4` in this case) specifies how many parallel test executions to run. This helps to speed up large test suites.

---

### 13. **Generate a JUnit XML Report**
   ```bash
   pytest --junitxml=report.xml
   ```
   **Explanation:** Creates a JUnit XML-style report, which is useful for integrating with CI/CD pipelines that require test result formats. The results are saved in `report.xml`.

### 14. **Generate a Coverage Report (Using pytest-cov Plugin)**
   ```bash
   pytest --cov=path/to/code_directory --cov-report=html
   ```
   **Explanation:** Measures code coverage for the tests and generates an HTML report. This helps in analyzing which parts of the codebase are being tested and which are not.

---

### 15. **Mark Tests with Custom Markers**
   ```bash
   pytest -m marker_name
   ```
   **Explanation:** Runs only tests that have been marked with a custom marker. For example, if certain tests are marked as "slow," you can run them selectively:
   ```bash
   pytest -m "slow"
   ```
   (Custom markers need to be registered in the `pytest.ini` file.)

### 16. **Show Reasons for Skipped Tests and Warnings**
   ```bash
   pytest -rs
   ```
   **Explanation:** Shows a summary of the reasons for any skipped tests and warnings. This is useful for debugging why certain tests were skipped or failed to execute.

### 17. **Run Only Failed Tests from the Last Session**
   ```bash
   pytest --lf
   ```
   **Explanation:** Re-runs only the tests that failed in the previous test run. This is a quick way to focus on the problematic tests from the last session.

### 18. **Re-run Failed Tests (With Retries)**
   ```bash
   pytest --reruns 3
   ```
   **Explanation:** This re-runs any tests that failed, up to a specified number of retries (e.g., 3). It's useful when tests might fail intermittently due to environmental or external factors.

---

### 19. **Run Tests with pdb (Python Debugger) on Failure**
   ```bash
   pytest --pdb
   ```
   **Explanation:** Automatically launches the Python debugger (`pdb`) on any test failure. This allows for real-time debugging when a test case fails.

### 20. **Run pytest in a Specific Environment**
   ```bash
   pytest --env=ENV_NAME
   ```
   **Explanation:** Runs the tests in a specific environment (e.g., a virtual environment). This helps in testing code under different environment settings.

### 21. **Run Tests with Warnings Displayed as Errors**
   ```bash
   pytest -W error
   ```
   **Explanation:** Treats all warnings as errors, causing the test suite to fail if any warning is encountered. This is useful for ensuring that the codebase doesn’t have hidden warnings that could cause problems later.

---

By understanding these pytest commands and their explanations, you can effectively manage and debug Python test suites, speeding up the development and testing process.