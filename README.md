# nextest-json-suite-overwrite

To reproduce:
1. Clone the repo
2. Run `cargo nextest list`
3. Run `cargo nextest list -T json-pretty`

The list output is correct:
```
nextest-json-suite-overwrite:
    tests::test_bin
nextest-json-suite-overwrite:
    tests::test_lib
```

The JSON only includes one test because the suites have the same name:
```
{
  "test-count": 2,
  "rust-suites": {
    "nextest-json-suite-overwrite": {
      "package-name": "nextest-json-suite-overwrite",
      "binary-name": "nextest-json-suite-overwrite",
      "package-id": "nextest-json-suite-overwrite 0.1.0 (path+file:///home/psanford/dev/personal/nextest-json-suite-overwrite)",
      "binary-path": "/home/psanford/dev/personal/nextest-json-suite-overwrite/target/debug/deps/nextest_json_suite_overwrite-f6e5ec81cf47d26a",
      "cwd": "/home/psanford/dev/personal/nextest-json-suite-overwrite",
      "testcases": {
        "tests::test_lib": {
          "ignored": false,
          "filter-match": {
            "status": "matches"
          }
        }
      }
    }
  }
}
```

All tests are correctly run:
```
    Finished test [unoptimized + debuginfo] target(s) in 0.00s
    Starting 2 tests across 2 binaries
        PASS [   0.001s] nextest-json-suite-overwrite tests::test_lib
        PASS [   0.001s] nextest-json-suite-overwrite tests::test_bin
     Summary [   0.002s] 2 tests run: 2 passed, 0 skipped
```
