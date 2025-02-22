## Changes

# 3.0.0 / 2019-10-18

### Notes

* [FEATURE] Add a way to configure the maximum size of a single payload (was always 1432, the optimal size for local UDP). See [#91][].
* [IMPROVEMENT] Various performance improvements. See [#91][].
* [OTHER] The client now pre-allocates 4MB of memory to queue up metrics. This can be controlled using the [WithBufferPoolSize](https://godoc.org/github.com/DataDog/datadog-go/statsd#WithBufferPoolSize) option.

### Breaking changes

- Sending a metric over UDS won't return an error if we fail to forward the datagram to the agent. We took this decision for two main reasons:
  - This made the UDS client blocking by default which is not desirable
  - This design was flawed if you used a buffer as only the call that actually sent the buffer would return an error
- The `Buffered` option has been removed as the client can only be buffered. If for some reason you need to have only one dogstatsd message per payload you can still use the `WithMaxMessagesPerPayload` option set to 1.
- The `AsyncUDS` option has been removed as the networking layer is now running in a separate Goroutine.

# 2.3.0 / 2019-10-15

### Notes

 * [IMPROVEMENT] Use an error constant for "nil client" errors. See [#90][]. Thanks [@asf-stripe][].

# 2.2.0 / 2019-04-11

### Notes

 * [FEATURE] UDS: non-blocking implementation. See [#81][].
 * [FEATURE] Support configuration from standard environment variables. See [#78][].
 * [FEATURE] Configuration at client creation. See [#82][].
 * [IMPROVEMENT] UDS: change Mutex to RWMutex for fast already-connected path. See [#84][]. Thanks [@KJTsanaktsidis][].
 * [IMPROVEMENT] Return error when using on nil client. See [#65][]. Thanks [@Aceeri][].
 * [IMPROVEMENT] Reduce `Client.format` allocations. See [#53][]. Thanks [@vcabbage][].
 * [BUGFIX] UDS: add lock to writer for concurrency safety. See [#62][].
 * [DOCUMENTATION] Document new options, non-blocking client, etc. See [#85][].
 * [TESTING] Adding go 1.10 and go 1.11 to CI. See [#75][]. Thanks [@thedevsaddam][].

# 2.1.0 / 2018-03-30

### Notes

 * [IMPROVEMENT] Protect client methods from nil client. See [#52][], thanks [@ods94065][].

# 2.0.0 / 2018-01-29

### Details

Version `2.0.0` contains breaking changes and beta features, please refer to the
_Notes_ section below for details.

### Notes

 * [BREAKING] `statsdWriter` now implements io.Writer interface. See [#46][].
 * [BUGFIX] Flush buffer on close. See [#47][].
 * [BETA] Add support for global distributions. See [#45][].
 * [FEATURE] Add support for Unix Domain Sockets. See [#37][].
 * [FEATURE] Export `eventAlertType` and `eventPriority`. See [#42][], thanks [@thomas91310][].
 * [FEATURE] Export `Flush` method. See [#40][], thanks [@colega][].
 * [BUGFIX] Prevent panics when closing the `udsWriter`. See [#43][], thanks [@jacek-adamek][].
 * [IMPROVEMENT] Fix issues reported by Golint. See [#39][], thanks [@tariq1890][].
 * [IMPROVEMENT] Improve message building speed by using less `fmt.Sprintf`s. See [#32][], thanks [@corsc][].

# 1.1.0 / 2017-04-27

### Notes

* [FEATURE] Export serviceCheckStatus allowing interfaces to statsd.Client. See [#19][] (Thanks [@Jasrags][])
* [FEATURE] Client.sendMsg(). Check payload length for all messages. See [#25][] (Thanks [@theckman][])
* [BUGFIX] Remove new lines from tags. See [#21][] (Thanks [@sjung-stripe][])
* [BUGFIX] Do not panic on Client.Event when `nil`. See [#28][]
* [DOCUMENTATION] Update `decr` documentation to match implementation. See [#30][] (Thanks [@kcollasarundell][])

# 1.0.0 / 2016-08-22

### Details

We hadn't been properly versioning this project. We will begin to do so with this
`1.0.0` release. We had some contributions in the past and would like to thank the
contributors [@aviau][], [@sschepens][], [@jovanbrakus][],  [@abtris][], [@tummychow][], [@gphat][], [@diasjorge][],
[@victortrac][], [@seiffert][] and [@w-vi][], in no particular order, for their work.

Below, for reference, the latest improvements made in 07/2016 - 08/2016

### Notes

* [FEATURE] Implemented support for service checks. See [#17][] and [#5][]. (Thanks [@jovanbrakus][] and [@diasjorge][]).
* [FEATURE] Add Incr, Decr, Timing and more docs.. See [#15][]. (Thanks [@gphat][])
* [BUGFIX] Do not append to shared slice. See [#16][]. (Thanks [@tummychow][])

<!--- The following link definition list is generated by PimpMyChangelog --->
[#5]: https://github.com/DataDog/datadog-go/issues/5
[#15]: https://github.com/DataDog/datadog-go/issues/15
[#16]: https://github.com/DataDog/datadog-go/issues/16
[#17]: https://github.com/DataDog/datadog-go/issues/17
[#19]: https://github.com/DataDog/datadog-go/issues/19
[#21]: https://github.com/DataDog/datadog-go/issues/21
[#25]: https://github.com/DataDog/datadog-go/issues/25
[#28]: https://github.com/DataDog/datadog-go/issues/28
[#30]: https://github.com/DataDog/datadog-go/issues/30
[#32]: https://github.com/DataDog/datadog-go/issues/32
[#37]: https://github.com/DataDog/datadog-go/issues/37
[#39]: https://github.com/DataDog/datadog-go/issues/39
[#40]: https://github.com/DataDog/datadog-go/issues/40
[#42]: https://github.com/DataDog/datadog-go/issues/42
[#43]: https://github.com/DataDog/datadog-go/issues/43
[#45]: https://github.com/DataDog/datadog-go/issues/45
[#46]: https://github.com/DataDog/datadog-go/issues/46
[#47]: https://github.com/DataDog/datadog-go/issues/47
[#52]: https://github.com/DataDog/datadog-go/issues/52
[#53]: https://github.com/DataDog/datadog-go/issues/53
[#62]: https://github.com/DataDog/datadog-go/issues/62
[#65]: https://github.com/DataDog/datadog-go/issues/65
[#75]: https://github.com/DataDog/datadog-go/issues/75
[#78]: https://github.com/DataDog/datadog-go/issues/78
[#81]: https://github.com/DataDog/datadog-go/issues/81
[#82]: https://github.com/DataDog/datadog-go/issues/82
[#84]: https://github.com/DataDog/datadog-go/issues/84
[#85]: https://github.com/DataDog/datadog-go/issues/85
[#90]: https://github.com/DataDog/datadog-go/issues/90
[@Aceeri]: https://github.com/Aceeri
[@Jasrags]: https://github.com/Jasrags
[@KJTsanaktsidis]: https://github.com/KJTsanaktsidis
[@abtris]: https://github.com/abtris
[@aviau]: https://github.com/aviau
[@colega]: https://github.com/colega
[@corsc]: https://github.com/corsc
[@diasjorge]: https://github.com/diasjorge
[@gphat]: https://github.com/gphat
[@jacek-adamek]: https://github.com/jacek-adamek
[@jovanbrakus]: https://github.com/jovanbrakus
[@kcollasarundell]: https://github.com/kcollasarundell
[@ods94065]: https://github.com/ods94065
[@seiffert]: https://github.com/seiffert
[@sjung-stripe]: https://github.com/sjung-stripe
[@sschepens]: https://github.com/sschepens
[@tariq1890]: https://github.com/tariq1890
[@theckman]: https://github.com/theckman
[@thedevsaddam]: https://github.com/thedevsaddam
[@thomas91310]: https://github.com/thomas91310
[@tummychow]: https://github.com/tummychow
[@vcabbage]: https://github.com/vcabbage
[@victortrac]: https://github.com/victortrac
[@w-vi]: https://github.com/w-vi
[@asf-stripe]: https://github.com/asf-stripe
