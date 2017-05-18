# SwiftlintWarnings
This is a repository describing how swift lint warnings fail to show up when piped through xcpretty(fastlane style)


#Walkthrough:
1. Clone the repository, go into it's root directory.
2. Compile the app with Xcode observe 7 warnings.
3. (Optional) run swift lint in the same directory, observe 7 warnings as well.
4. Run `fastlane scan` in the same repository, see that warnings are not shown in the output. 
5. Run the underlying command that fastlane invokes without piping to xcpretty and observe the 7 warnings being thrown `xcodebuild -scheme SwiftlintXcpretty -project ./SwiftlintXcpretty.xcodeproj build test`
6. Conclusion: xcpretty(0.2.4) might be filtering out the output of swiftlint.
```fastlane 2.30.1,
swiftlint version 0.18.1
[10:33:24]: ▸ Loading...
[10:33:24]: ▸ Building SwiftlintXcpretty/SwiftlintXcpretty [Debug]
[10:33:24]: ▸ Check Dependencies
[10:33:24]: ▸ Running script 'SwiftLint analyzer'
[10:33:24]: ▸ Build Succeeded
[10:33:24]: ▸ Building SwiftlintXcpretty/SwiftlintXcpretty [Debug]
[10:33:24]: ▸ Check Dependencies
[10:33:25]: ▸ Running script 'SwiftLint analyzer'
[10:33:25]: ▸ Building SwiftlintXcpretty/SwiftlintXcprettyTests [Debug]
[10:33:25]: ▸ Check Dependencies
[10:33:25]: ▸ Running script 'Run Script'
[10:33:25]: ▸ Building SwiftlintXcpretty/SwiftlintXcprettyUITests [Debug]
[10:33:25]: ▸ Check Dependencies
[10:33:30]: ▸ All tests
[10:33:30]: ▸ Test Suite SwiftlintXcprettyTests.xctest started
[10:33:30]: ▸ SwiftlintXcprettyTests
[10:33:30]: ▸ ✓ testExample (0.001 seconds)
[10:33:30]: ▸ ◷ testPerformanceExample measured (0.000 seconds)
[10:33:30]: ▸ ✓ testPerformanceExample (0.312 seconds)
[10:33:30]: ▸ 	 Executed 2 tests, with 0 failures (0 unexpected) in 0.313 (0.315) seconds
[10:33:30]: ▸
[10:33:37]: ▸ All tests
[10:33:37]: ▸ Test Suite SwiftlintXcprettyUITests.xctest started
[10:33:37]: ▸ SwiftlintXcprettyUITests
[10:33:43]: ▸ ✓ testExample (6.202 seconds)
[10:33:43]: ▸ 	 Executed 1 test, with 0 failures (0 unexpected) in 6.202 (6.205) seconds
[10:33:43]: ▸
[10:33:43]: ▸ Test Succeeded
+--------------------+---+
|      Test Results      |
+--------------------+---+
| Number of tests    | 3 |
| Number of failures | 0 |
+--------------------+---+
```
