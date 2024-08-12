# TODOs for -04

## Based on Bill Fenner's Review:
- Clarify in the doc, like in the Introduction section that there is no “as opposed to” dichotomy, and instead the wholistic view as well as the on-demand path-specific view are both useful, for different purposes and use cases. The key, of course, is that the values reported in both cases are consistent.

- Add this in the limitation that this object cann ot be added to extended echo. (As described by https://datatracker.ietf.org/doc/draft-fenner-intarea-probe-clarification/ due to implementations adding arbitrary data, RFC8335 only permits the single extension object for extended echo, so this object can't be added to extended echo at all.)

- Due to 32-bit unsiegned work being small for node an component-level throughput (high interface speeds), it's too small to represent most interface speeds. So, we should make a new Sub-Object which is a 64-bit unsigned word for every respective 32-bit sub-object. Or just have one 64-bit unsigned word which can also accomodate a smaller 32 bit data?
(If we have two size options in the sub-obects then can the device choose what size of sub-object to add to the message based on the size of the data)

- Clarify about mapping UUIDs to the component/node. (example: node will be the IP address and UUID==0, components will be printed with the value and not the mapping)