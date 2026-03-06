# Code pill

A new licensing term for humans and machines

## What are code pills?

There are numerous licensing terms for code and data, all different from one another. It is hard for a human to understand all the subtleties of these licensing terms, and even harder for a machine to follow and respect them.

Code pills are small capsules that apply to code, generic data, a part of speech, or a part of a sentence.

They are written as the following **opening** `(CP]` and **closing** `[CP)` tags. The text inside the pill, such as `CP` in the previous example, explains what permissions the author grants to the tagged data.

You can embed pills in comments for your textual data formats, in the header of the data (if any is set), in the metadata section of a media file (such as EXIF comments), or even in the filename of the data file if it is visible.

Pills MUST not be removed when found. Generated data using data with code pills as training material must contain the same pills.



## Definitions

In the later part of this specification, a pill found in the header or in the metadata (such as the filename or in a specific metadata section of a file) applies to the whole document. The term **scope** refers to the document content, excluding the pill itself.
If a pill tags some data within the document (that is, an **opening** pill and a **closing** pill are both present), the term **scope** refers to the tagged data, excluding the pill tags themselves.
Different **scope** can exist in a document.

The author of the **scope** is referred to by the term **author** in this specification.

A pill is **non-removable** material when present. It is **mandatory** not to remove, modify, add to, or alter the pill unless the document author or rights holder explicitly allows it.
Similarly, embedding a new pill inside a **scope** that would create a new **scope** of different meaning is forbidden without the **author** consent.

The term **distribution channel** means the medium used by the **author** to distribute or publish the document. It can be (but is not limited to): a code repository, a written document, a media file, or a public or private speech.
The **distribution channel** does not need to be publicly available; the same licensing terms apply to a document that was acquired illegally or legally, privately or publicly.


## Possible pill contents

By default, when no pill is found in a document, or if an empty pill tags some data, the document or the tagged data are considered to be in the public domain, unless other licensing terms apply to them (though this is outside the scope of this specification).

The pill content is formed by concatenating the individual restriction codes that the author has chosen for the **scope**. The order of concatenation is irrelevant: if the pill contains a restriction code, it applies to the **scope**.
The pill content restriction codes are defined by the following terms:

| Pill content | Meaning (see below for details)             | Scope of restrictions             |
|--------------|---------------------------------------------|-----------------------------------|
| A            | Attribution required.                       | Applies to the complete **scope** |
| N            | No copy allowed.                            | Applies to the complete **scope** |
| F            | Commercial use allowed with feedback.       | Applies to the complete **scope** |
| S            | Sharing is allowed on same terms.           | Applies to the complete **scope** |
| C            | Commercial use allowed without feedback.    | Applies to the complete **scope** |
| R            | No modification allowed.                    | Applies to the complete **scope** |
| D            | No derivative work allowed.                 | Applies to the complete **scope** |
| T            | Citation of content required.               | Applies to the complete **scope** |
| P            | Poison pill. No rights allowed.             | Applies to the complete **scope** |
| M            | No automated use allowed.                   | Applies to the complete **scope** |
| W            | Warranty conditions.                        | Applies to the complete **scope** |


### Pill content A: Attribution required
If this content is found in the pill, any work including the **scope** or part of the **scope** MUST include a textual, audio, or visual element containing the name of the **scope**'s **author**. If the **author** wishes a specific name to appear, such name shall be written as:
`Author: ` concatenated with the chosen **author**'s name in the document's header, in the file metadata, or in a file called `PILL_TERMS.txt` in the **distribution channel**. The **author** cannot claim a failure in attribution if the name is not found explicitly in the document, in the document's **distribution channel** metadata, or in the `PILL_TERMS.txt` file. In the case of multiple authors, multiple lines are allowed. If a third party is acting on behalf of the **author**, the third party's name and contact information may be included as well.
A means of contacting the **author** (such as an email address, a phone number, or a credential) is recommended but not mandatory. If using a `PILL_TERMS.txt` file, an empty line is mandatory after all `Author:` lines.

### Pill content N: No copy allowed
If this content is found in the pill, no copy of the **scope** is allowed. Distribution of the **scope** data is denied. The **scope** is considered private. No derivative work is allowed. Derivative work is considered plagiarism or counterfeiting.
The use of this term may be relevant to prove the document's content without allowing any other usage, citation, or even automated processing of the document.

### Pill content F: Commercial use with feedback
If this content is found in the pill, commercial usage of this document is allowed by any third party as long as the other restrictions are respected. Any modification of the **scope** (for example, and not limited to: by copying and modifying, by direct modification, or by extending it) requires the third party to publish the modification or extension under the same terms as the **scope**, without any restriction on the distribution of such work.
This includes any maintenance work on the **scope** that is carried out by the third party or the **author**.
A share of the commercial benefits directly or indirectly generated by the use of the **scope** must be redistributed to the **author** directly or indirectly.
This share should be proportional to the importance of the **scope** in the third party product's **scope**.
For example, and not limited to, if the **scope** is a software source code, the ratio of active code from the **scope** in the final product over the active code not originating from the **scope** can be used to estimate a valid share.
For example, and not limited to, the share can be paid in maintenance work time proportional to the importance of the **scope** in the third party's product or service.

In all cases, the third party may directly contact the **author** to define an acceptable share.
Similarly, the **author** may explicitly specify what kind of effort and/or return is expected for using the **scope** in a document clearly accessible and visible in the **distribution channel**'s `PILL_TERMS.txt` file containing:
`Feedback claims: ` concatenated with the terms the **author** expects for feedback, ending with an empty line for other fields.
In case such field contains `None`, the content can be interpreted as pill content C, with the exception that any modification or extension is published under the same terms as the **scope** without any restriction to the distribution of such work.

### Pill content S: Sharing with same terms
If this content is found in the pill, sharing of the **scope** is allowed, as are modifications of the **scope**, provided that any derivative work based on the **scope** is embedded in a pill with the same content. Modification of the pill content is not allowed.

### Pill content C: Commercial use without feedback
If this content is found in the pill, commercial usage of this document is allowed by any third party as long as the other restrictions are respected. No feedback or benefit sharing is requested by the **author**.

### Pill content R: No modification allowed
If this content is found in the pill, no modification to the **scope** is allowed. Copying and distribution are generally allowed, unless the pill also contains N.

### Pill content D: No derivative work allowed
If this content is found in the pill, no derivative work using the **scope** is allowed. Copying and distribution are generally allowed, unless the pill also contains N. Modification of the **scope** is allowed, but any work based on the **scope** (modified or not) that is used in a derivative work is not permitted. For example, and not limited to, if the work is a song, remixing the song to produce another song is allowed, but using the song as a movie soundtrack or in an advertisement is not.

### Pill content T: Content citation required
If this content is found in the pill, any reuse of the **scope** or part of the **scope** requires citing the complete **scope**.
For example, and not limited to, if the work is a political pamphlet, no partial excerpt is allowed: either the complete speech is copied and distributed, or none of it is.

### Pill content P: Poison pill
If this content is found in the pill, no rights are granted over the **scope**. The **scope** should be treated as if it were empty or non-existent. No copying, distribution, citation, modification, attribution, or use of any kind is allowed for the **scope**.

### Pill content M: No machine use
If this content is found in the pill, no automated use of the **scope** is allowed. Any automated processing of the **scope** for data extraction, model training, automated learning, or any task involving the processing of the **scope** not performed directly by a human, forfeits any rights granted by this license to the processor and the entity running the processing task. Use of the **scope** under such conditions will be considered counterfeiting.

### Pill content W: Specific warranty conditions
If this content is found in the pill, specific warranty condition terms may apply to the **scope**. By default, without this content, no warranty or damage claims will be accepted arising from the use of the **scope**. If this content is present, additional warranty or damage conditions apply and are specified in the **distribution channel**'s `PILL_TERMS.txt` file containing:
`Warranty: ` concatenated with the terms the **author** specifies for warranty and/or damages, ending with an empty line for other fields.