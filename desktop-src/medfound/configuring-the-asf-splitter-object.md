---
Description: Configuring the ASF Splitter Object
ms.assetid: 8e2ba659-e1f6-42be-afd6-21fc841dc8d3
title: Configuring the ASF Splitter Object
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# Configuring the ASF Splitter Object

The ASF *splitter* object is a WMContainer layer object that parses the ASF Data Object of an Advanced Systems Format (ASF) file. After the splitter is created and initialized to parse the ASF Data Object of a media file, the splitter must be configured to generate samples for specific streams. Call [**IMFASFSplitter::SelectStreams**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-selectstreams) to select the required streams.

Optionally, an application can also configure it to generate samples in reverse order or generate samples for protected content. To set these options, call [**IMFASFSplitter::SetFlags**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-setflags) and pass the required bitwise combination of the supported flags. Before calling this method, the client must complete the [**IMFASFSplitter::Initialize**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-initialize) call successfully; otherwise, **SetFlags** fails with **MF\_E\_NOT\_INITIALIZED** error code. For information about initializing the splitter, see [Creating the ASF Splitter Object](creating-the-asf-splitter-object.md).

To check whether this flag is currently set on the splitter, call [**IMFASFSplitter::GetFlags**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-getflags).

## Selecting Streams for Parsing

During the initialization process through [**IMFASFSplitter::Initialize**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-initialize) call, the splitter detects the number of streams and the stream identifiers in the ASF file. By default, no streams are selected by the splitter. The application must select the streams by calling [**IMFASFSplitter::SelectStreams**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-selectstreams). This method takes an array of stream numbers. To get the stream number for a stream, call [**IMFASFProfile::GetStream**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfprofile-getstream) on the ASF profile or call [**IMFStreamDescriptor::GetStreamIdentifier**](/windows/desktop/api/mfidl/nf-mfidl-imfstreamdescriptor-getstreamidentifier) on the stream descriptor. (You can obtain both the ASF profile and the stream descriptor from the ContentInfo object.) If the client passes a stream number that is not recognized by the splitter, it fails with a **MF\_E\_INVALIDSTREAMNUMBER** error.

Calling [**SelectStreams**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-selectstreams) clears the previous selections. Any stream that is not specified in the array is not selected. To get a list of streams that are currently selected, call [**IMFASFSplitter::GetSelectedStreams**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-getselectedstreams). This method takes a pointer to an array, which the method fills with the stream numbers. If the array size is less than the number of selected streams, the method fails with the **MF\_E\_BUFFERTOOSMALL** error. In this case, the method returns the number of selected streams in the *pwNumStreams* parameter. You can then use this number to allocate an array of the correct size and call the method again.

For example code, see "Select a Stream for Parsing" in [Tutorial: Reading an ASF File](tutorial--reading-an-asf-file.md).

## Reverse Playback Setting

During the initialization process of the splitter, it determines if the ASF content supports reverse playback. If it does, the splitter can be configured to generate samples in reverse order by setting the **MFASF\_SPLITTER\_REVERSE** flag. If the content does not support reverse playback, the [**IMFASFSplitter::SetFlags**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-setflags) returns **MF\_E\_INVALIDREQUEST**, but the flag is set on the splitter.

If the splitter is configured to parse in the reverse direction, then the splitter always starts parsing at the end of the buffer that contains the ASF Data Object. Therefore, for reverse parsing the data offset and the length of the data to parse must be set appropriately. For information about setting the correct values, see [Generating Stream Samples from an Existing ASF Data Object](generating-stream-samples-from-an-existing-asf-data-object.md).

## Protected Content Setting

The splitter can be configured to work with packet-level encryption content by setting the **MFASF\_SPLITTER\_WMDRM** through [**IMFASFSplitter::SetFlags**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfsplitter-setflags). This instructs the splitter to deliver samples for content that is protected by Windows Media Digital Rights Management (DRM). When this flag is set, the samples generated by the splitter contain information required to decrypt media data and reconstruct the frames, such as the [**MFSampleExtension\_PacketCrossOffsets**](mfsampleextension-packetcrossoffsets-attribute.md) attribute. This attribute is a blob that contains an array of **DWORD**s. Each **DWORD** provides you the payload boundaries for the frame relative to the beginning of the frame. If this attribute is not present, the frame is contained in a single payload. Typically, the samples generated by the splitter contain multiple media buffers, the application can copy all the buffers into one contiguous buffer by calling [**IMFSample::ConvertToContiguousBuffer**](/windows/desktop/api/mfobjects/nf-mfobjects-imfsample-converttocontiguousbuffer). The resulting buffer contains the frame and the attribute value contains offsets into this buffer.

## Related topics

<dl> <dt>

[ASF Splitter](asf-splitter.md)
</dt> </dl>

 

 


