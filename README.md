
# Code pill

A licensing scheme for humans and machines — specification version 1.


[Interactive license content here](https://x-ryl669.github.io/codepill)

## What are code pills?

There are numerous licensing terms for code and data, all different from one another. It is hard for a human to understand all the subtleties of these licensing terms, and even harder for a machine to follow and respect them.

Code pills are small capsules that apply to code, generic data, a document, a part of a document, a part of a speech, or a part of a sentence.

A pill is written as an **opening** tag such as `(1ACM]` and, when needed, a matching **closing** tag such as `[1ACM)`. The letters inside the pill (here `A`, `C` and `M`) tell what the author asks in exchange for using the tagged content.

The principle fits in one sentence:

> **A pill grants every right the author can legally grant. Each letter in the pill takes some freedom back.**

So `(1]` (an empty pill) means "do what you want with it", `(1A]` means "do what you want, but credit me", and `(1ACM]` means "credit me, no commercial use, no machine processing".

You can embed pills in comments of textual data formats, in the header of the data (if any), in the metadata section of a media file (such as EXIF comments), in the file name when it is visible, or say them aloud in a speech.



## Definitions

The key words "MUST", "MUST NOT", "SHOULD", "SHOULD NOT" and "MAY" are to be interpreted as described in RFC 2119.

**Pill**: an opening tag, optionally followed later by its closing tag, as defined in the [Syntax](#syntax) section.

**Scope**: the content a pill applies to, excluding the pill tags themselves.
- A pill found in the header or in the metadata of a document (such as the file name or a specific metadata section of a file) applies to the whole document: the **scope** is the document content.
- A pill tagging some data within the document applies to the tagged data, from the opening tag to its closing tag (or to the end of the document if there is no closing tag).
- Several **scopes** can exist in a document, and **scopes** can be nested.

**Author**: the author (or rights holder) of the **scope**.

**User**: anyone, human or organisation, who uses the **scope** in any way, including through an automated process they run or commission.

**Distribution channel**: the medium used by the **author** to distribute or publish the document. It can be (but is not limited to): a code repository, a written document, a website, a media file, or a public or private speech.
The **distribution channel** does not need to be publicly available: the same terms apply to a document whether it was acquired legally or illegally, privately or publicly.

**Effective letters**: the set of letters that applies to a given part of a document, once all enclosing pills are taken into account (see [Nesting](#nesting)).

**Applicable law**: the copyright and authors' rights law that applies to the use, including its statutory exceptions (such as quotation) and the author's moral rights.



## Relationship with the law

- **No pill**: when no pill is found, this specification does not apply. The content is protected by the applicable law, which, in nearly every country (Berne Convention), means *all rights reserved*.
- **Empty pill**: `(1]` grants every economic right the **author** is legally able to grant. Rights the **author** cannot give away under the applicable law (for example, inalienable moral rights such as the right to integrity in France) remain with the **author**. The term "public domain" is deliberately not used, since it has different meanings in different countries.
- **Letters**: each letter is a condition attached to that grant. A **user** who does not respect a condition is not granted any right by the pill over the **scope**: the use is then governed by the applicable law alone.
- **Statutory exceptions**: a pill cannot remove a right that the applicable law gives to everyone (such as the right of quotation or fair use). Letters restrict what the pill *grants*, not what the law *allows*.
- **Other licences**: a document can also be distributed under another licence. Each licence is an independent grant and this specification does not combine with others. **Authors** SHOULD avoid contradictory statements.



## Syntax

```
opening  = "(" [ version ] letters [ "~" id ] "]"
closing  = "[" [ version ] letters [ "~" id ] ")"
version  = 1*DIGIT                          ; "1" for this specification
letters  = *ALPHA                           ; see "Pill letters" for their meaning
id       = 1*( ALPHA / DIGIT / "-" / "_" / "." )
```

Examples: `(1A]`, `(1ACM~photos]`, `(1]`, `(m]`, `[1ACM~photos)`.

- The pill only uses characters that are valid in file names on common systems (no `:`, `|`, `!`, `/`…), so it can appear in a file name as is.
- The version is the number at the start of the pill: `(1ACM]` is version 1 with the letters `A`, `C` and `M`. The empty pill of version 1 is `(1]`.
- The outermost pill of a document MUST carry the version. Pills nested inside a versioned **scope** MAY omit it: they inherit it. Tools SHOULD NOT treat an unversioned pill as a pill unless it is inside a versioned **scope**, to avoid confusion with ordinary text.
- A pill is interpreted with the meaning its version gives to each letter. Letters that this version does not define are ignored: since the version is part of the pill, a new letter introduced by a later version cannot be confused with a mistake.
- A processor that does not know the version of a pill MUST interpret the whole document as if its only pill were `(N]`: no use is granted except proving authenticity, date or authorship.
- The scope name uses `~` because it is valid in file names and in URLs, where `#` would start a fragment and `@` has a special meaning.
- The order of letters is irrelevant. Repeating a letter has no additional effect.
- The optional `~id` names the **scope**, so that its terms can be found in the `PILL_TERMS.txt` file (see [PILL_TERMS.txt](#pill_termstxt)).
- A closing tag MUST repeat exactly the content of the opening tag it closes, and closes the innermost open **scope**. It releases the letters that this opening tag added.
- A pill covering a whole document does not need a closing tag. A closing tag becomes functionally required as soon as the document may be included in another one (for example, a C header file included in another source file, or a paragraph pasted in another text).
- A closing tag that does not match the innermost open pill is ignored: the open pill keeps applying, up to the end of the document if needed.
- In a speech, the speaker says the pill aloud (for example "code pill one, A C M") at the beginning of the **scope**, and announces its end if the **scope** ends before the speech does. In a video, the pill MAY instead be displayed visibly for the whole **scope** (on screen, on a badge…).



## Pill letters

All letters apply to the complete **scope**. Uppercase letters take a freedom back. Lowercase letters are only meaningful in a nested pill, where they give back a freedom that an enclosing pill took (see [Nesting](#nesting)).

| Letter | Name                          | What it takes back                                                                           |
|--------|-------------------------------|----------------------------------------------------------------------------------------------|
| A      | Attribution                   | Using the **scope** without crediting the **author**.                                        |
| C      | No commercial use             | Any commercial use.                                                                          |
| D      | Distinct works only           | Reusing the **scope**, or recognizable parts of it, in another work.                          |
| F      | Feedback for commercial use   | Commercial use without a prior agreement with the **author** on retribution.                 |
| M      | No machine use                | Automated processing that is not for immediate human consumption.                            |
| N      | No use (proof only)           | Every use, except proving the authenticity, date or authorship of the **scope**.             |
| P      | Poison                        | Every use, including attribution: the **scope** is disowned and must be treated as noise.    |
| R      | No modification               | Modifying the **scope**: only verbatim copies are allowed.                                    |
| S      | Share alike                   | Distributing a work based on the **scope** under any other terms than the very same pill.     |
| T      | Truthful quotation            | Quoting the **scope** partially, without credit, or in a way that alters its meaning.         |
| W      | Warranty (informative)        | Nothing: it signals that specific warranty terms apply.                                       |


### A: Attribution
Any work including the **scope** or part of the **scope** MUST include a textual, audio, or visual element containing the name of the **author**.

The name to use is given by an `Author:` field, in the document's header, in the file metadata, or in the `PILL_TERMS.txt` file of the **distribution channel**. Multiple `Author:` fields are allowed. If a third party is acting on behalf of the **author**, its name and contact information MAY be given in an `Agent:` field.
The **author** cannot claim a failure in attribution if the name is not found explicitly in one of these places.
A means of contacting the **author** (an email address, a website…) is recommended but not mandatory, using a `Contact:` field.

### C: No commercial use
The **scope** MUST NOT be used commercially: it MUST NOT be sold, included in a product or service that is sold or that generates revenue (including through advertising), or used in the course of a for-profit activity.

If both `C` and `F` are present, `C` wins: no commercial use is granted.

### D: Distinct works only
The **scope** MUST NOT be reused as is, nor included in a larger work, nor reused through recognizable parts of it. A **user** MAY create a new work inspired by the **scope**, provided it is transformed so much that there is no possible doubt that it is not the original work.

Copying and distributing the **scope** itself, unchanged and on its own, remains allowed unless other letters say otherwise.

For example, if the **scope** is a song: sharing the song is allowed; composing a new song whose inspiration cannot be recognized is allowed; using the song (or a recognizable sample of it) in a remix, a movie soundtrack, or an advertisement is not.

### F: Feedback for commercial use
Commercial use of the **scope** is only granted once the **user** and the **author** have concluded an agreement on how the value brought by the **scope** is returned to the **author**.

The rationale is simple: if a **user** builds a commercial activity on the **scope**, it is because the **scope** has value, and the **author** deserves to discuss how that value is shared. Without such an agreement, no commercial right is granted.

The **author** MAY describe what is expected in a `Feedback:` field of the `PILL_TERMS.txt` file, as a starting point for the discussion. For example, and not limited to:
- a share of the revenue directly or indirectly generated, proportional to the importance of the **scope** in the **user**'s product or service (for software, the ratio of active code coming from the **scope** in the final product is a possible estimate);
- maintenance or development work on the **scope**, in time proportional to that importance;
- a one-time payment, a donation, or any other form of return.

If the **author** cannot be reached, no agreement can be concluded and no commercial right is granted. **Authors** using `F` SHOULD therefore provide a `Contact:` field.

`F` does not require the **user** to publish modifications. If the **author** wants that too, the pill also contains `S`.

### M: No machine use
The following uses of the **scope** are forbidden: data extraction, machine-learning training, text and data mining, any processing that is not targeted at immediate human consumption, and any processing not intended by the **author**.

Are not concerned, because they only convey the **scope** to a human as intended: displaying, rendering, printing, transmitting, storing or backing up the **scope**, accessibility tools (such as a screen reader), and, for code, compiling and executing it.

For **users** subject to European Union law, `M` is a machine-readable reservation of rights in the sense of Article 4(3) of Directive (EU) 2019/790 (text and data mining opt-out).

### N: No use (proof only)
No use of the **scope** is granted, whatever the purpose: no copy, distribution, communication, quotation, modification, processing or derivative work.

The only exception is proving the authenticity of the **scope**: the **scope** MAY be kept, timestamped, fingerprinted (for example with a cryptographic hash), and presented to establish its existence, its date, or its authorship, for example to prove the anteriority of an invention.

Unlike `P`, the **author** fully claims the **scope** as their own work.

### P: Poison
The **scope** is disowned by the **author**: it is noise, decoy, or generated content that the **author** does not claim. It MUST be treated as if it were empty or non-existent: no copy, distribution, quotation, modification, processing or use of any kind is granted, and the **scope** MUST NOT be attributed to the **author** nor used as an expression of their work or opinions.

`P` exists for forensic purposes: since nobody is allowed to use a poisoned **scope**, finding it, or something recognizably derived from it, anywhere else (in another document, in a dataset, in the output of a model) proves that the pill was not respected.

`P` dominates every other letter.

### R: No modification
The **scope** MUST NOT be modified. Copying and distributing verbatim copies of the **scope** is allowed unless other letters say otherwise. Changing the format without changing the content (for example, re-encoding an image) is not a modification.

### S: Share alike
Any work that includes or is based on the **scope**, when distributed, MUST be distributed under a pill with exactly the same letters as the **scope**'s pill.

### T: Truthful quotation
Any partial reuse (quotation, excerpt) of the **scope** MUST:
- name the **author** and the source;
- be clearly identifiable as a quotation;
- not alter, distort or reverse the meaning of the **scope**, including by cutting it.

If the meaning of the **scope** depends on its whole, only the complete **scope** can be reused. For example, if the **scope** is a political pamphlet, an excerpt that makes it say something the complete pamphlet does not say is forbidden.

`T` strengthens, in the pill, the rules that most laws already attach to quotation (for example the French *droit de citation* and the author's right to the integrity of the work).

### W: Warranty
By default, without this letter, no warranty is given and no damage claim is accepted arising from the use of the **scope**.
If `W` is present, specific warranty or damage terms apply, described in a `Warranty:` field of the `PILL_TERMS.txt` file.

`W` does not take any freedom back: it is informative.



## Nesting

Pills can be nested. The effective letters of a nested **scope** are the effective letters of its enclosing **scope**, plus its uppercase letters, minus its lowercase letters.

```
(1ACM]               effective: A C M
  ...
  (m]                effective: A C      (machines may process this part)
    ...
    (R]              effective: A C R
    [R)              effective: A C
  [m)                effective: A C M
  ...
```

Only the **author** of a **scope** MAY add a pill inside it, and therefore only the **author** can relax a letter with a lowercase letter. A third party MUST NOT remove, modify, add to, or alter a pill.

A lowercase letter is a convenience: it avoids closing a pill, then opening it again, around the narrower part.



## Using pilled content

- **Pills are non-removable.** Any copy, excerpt, or work that includes or is based on a **scope** MUST carry the **scope**'s pill (with its closing tag when included in a larger work).
- **Letters add up.** When contents from several **scopes** are combined, the result carries all their pills, and the effective letters of the result are the union of their letters.
- **The most restrictive wins.** When two letters cannot both be satisfied, the one granting less applies: `P` dominates everything, then `N`, and `C` dominates `F`.
- **Incompatible combinations are forbidden.** Contents cannot be combined when their pills cannot all be respected together. In particular:
  - a **scope** with `N` or `P` cannot be combined with anything;
  - a **scope** with `D` cannot be included, recognizably, in a combination;
  - a **scope** with `S` can only be combined with **scopes** whose letters are all present in its own pill, and two `S` **scopes** can only be combined if they have exactly the same letters.
- **Generated content.** Content generated by a process that used pilled **scopes** (for example, a model trained on them) is a work based on those **scopes**: it MUST carry the combination of their pills. If the combination is incompatible, the output MUST be discarded. In practice, this means training datasets have to be separated into groups of compatible pills.



## PILL_TERMS.txt

The `PILL_TERMS.txt` file is a UTF-8 text file placed at the root of the **distribution channel** (for example, at the root of a code repository or a website). It holds the information some letters refer to.

- The file is made of records separated by an empty line.
- Each record is made of `Field: value` lines. A value can continue on the next lines, which then start with a space or a tab.
- A record starting with `Scope: <id>` applies to the pills with that `~id`. A record without a `Scope:` field applies to the pills without an `~id`.

| Field       | Used by | Content                                                                 |
|-------------|---------|-------------------------------------------------------------------------|
| `Scope:`    | all     | The `~id` of the pills this record applies to.                           |
| `Author:`   | A       | The name to credit. Can be repeated for multiple authors.                |
| `Agent:`    | A, F    | A third party acting on behalf of the **author**, with its contact.      |
| `Contact:`  | A, F    | A way to contact the **author**.                                          |
| `Feedback:` | F       | What the **author** expects in exchange for commercial use.               |
| `Warranty:` | W       | The warranty and/or damage terms.                                         |

Example:

```
Author: Jane Doe
Contact: jane@example.org

Scope: engine
Author: Jane Doe
Author: John Roe
Contact: engine@example.org
Feedback: 2% of the net revenue of any product shipping this engine,
  or equivalent maintenance time. Please contact us before shipping.

Scope: icons
Author: Studio Example
Warranty: The icons are guaranteed free of any third-party rights.
  The author covers documented claims up to 1000 EUR.
```



## FAQ

**Why does a pill grant everything by default, instead of reserving everything?**
Because the law already reserves everything when there is no pill. A pill is only useful to give rights away, and the most common wishes are then the shortest to write: `(1A]` for "credit me", `(1AS]` for "credit me and keep it open", `(1ACM]` for "credit me, not for profit, not for machines".

**Do I need a closing pill?**
Not for a whole document. You need one as soon as the protection changes inside a document, or when the document may be included in another one.

**How do I lift a restriction for a small part of my document?**
Use a nested pill with the lowercase letter, such as `(m]` inside a `(1ACM]` document. You can also close the pill and open a new one.

**What happens with an unknown letter?**
It is ignored. The pill carries its version, so a letter added by a later version is read with that version's specification, and a letter that no version defines has no meaning.

**What happens with a version I don't know?**
The whole document is read as `N`: nothing is granted until the tool knows that version. This way, a tool that is not up to date never grants a freedom that a newer letter takes back.

**Why a number and not `CP1:` as a prefix?**
A pill must survive in a file name. `:` is forbidden in Windows file names, and `|` or `!` are special characters in POSIX shells. A leading digit is valid everywhere and keeps the pill short: `(1ACM]`.

**What is the difference between `N` and `P`?**
With `N`, the **author** claims the work but keeps it private: it can only be used as proof of its existence, date, or authorship. With `P`, the **author** disowns the content: it is noise that must be ignored, and finding it anywhere else proves the pills were not respected.

**Can a pill forbid me to quote a text?**
No. The right of quotation granted by law (fair use, fair dealing, *droit de citation*…) is not given by the pill, so it cannot be taken back by the pill. `T` only makes the rules of a faithful quotation explicit.

**How do I put a pill in a speech or a video?**
Say it aloud when the **scope** starts (and when it ends if it ends before the speech does), or display it visibly for the whole **scope**.
