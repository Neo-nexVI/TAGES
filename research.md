# TAGES
TAG-Engine System

**Javonn Alleyne**
Barbados, 2026

# Abstract 
The TAG-Engine System, TAGES, is a lossy encoding system designed to take a single word and produce an opaque or non-intuitive alphabetical identifier, or TAG of three or five letters, referred to as a TRI-TAG or QUIN-TAG respectively. The goal was to produce a deterministic standardised naming scheme that can be applied to existing items without implying any hidden meaning or context, instead of a generalised name or container like existing conventional naming schemes. It creates a simple compact label derived from the input word.
The engine's algorithm follows a simple series of steps, making use of ASCII and binary conversions.

# Introduction
Why build the TAG-Engine? The TAG-Engine was built solely for the purpose of generating unique names or tags and assigning them to timelines in a fictional universe. Instead of going the standard route of timeline 1 timeline 2 or creating a perfectly crafted name that fits the aesthetics or thematic framing of the specific timeline in question, I designed a new system. The core ideas came from other works of fiction such as Marvel Comics, DC Comics and The Transformers Universe. My goal was to design a similar naming scheme to these media properties. The issue upon further inspection is that the names given to the timelines in their properties, mainly Marvel and DC were pseudo random. The ever so popular main Marvel universe, Earth-616, was a randomly chosen name. DC also follows the trend, with assigning a number to Earth, Earth 1, Earth 2, Earth 3, etc. These names, while readable, were not unique enough to standout and carry any significant information. Despite both companies being rivals they still follow the same naming convention of Earth + a number.

The only outstanding property to consistently name their timelines was The Transformers. Their multiverse, also known as the Universal Stream, was the main inspiration for the TAG-Engine. It features a combination of cluster names, Greek letters an publication dates to create a systematic, readable and interestingly unique identifier. An example of a full name would be Malgus 1023.4 Gamma, meaning A comic (Gamma) existing in the Animated continuity (Malgus) released on the 4th of October 2023 (1023.4). The naming convention is simple but provides a complex combination of ideas to form something unique. Therefore the TAG-Engine was designed to mimic a similar naming convention.

# Related Work 
## Deterministic Identifier Schemas
are mathematical data models and systems that produce identical outputs when given the same inputs. They rely on exact matching, using unique identifiers such as email addresses, userIDs or account numbers. Deterministic models have three key characteristics consistency, the same input always produces the same output, transparency, clear logic that can be easily audited and precision, binary yes/no decisions rather than probability outcomes.

## Universally Unique Identifier
is a 128-bit number, represented as a 36-character string in the format of 5 hex strings separated by hyphens, to identify information and resources in computer systems. GUID (Globally Unique Identifier) is an alternate form of the concept. One advantage of using UUIDs is that no centralised authority is required to administer them.

A UUID can be used for multiple purposes, from tagging objects with an extremely short lifetime, to reliably identifying very persistent objects across a network. UUIDv3 and UUIDv5 are deterministic hashing algorithms and are used for generating reproducible UUIDs. 
- Version 3 makes use of the MD5 hashing algorithm:
	MD5 (Message Digest 5) is a widely used casing function producing a 128-bit hash value. It takes a message of any input length and changes it into a fixed-length message of 16 bytes.

- Version 5 makes use of the SHA-1 hashing algorithm:
	SHA-1(Secure Hashing Algorithm 1) takes an input and produces a 160-bit hash value. SHA-1 is based on the design principles of the MD4 and MD5 algorithms

UUIDs are inherently very difficult to resolve in a global sense. This coupled with the fact that UUIDs are temporally unique within their spatial context, ensures that UUIDs will remain as persistent as possible.

## Baudot Code
is an early character encoding for telegraphy in the 1870s. It was the predecessor to the International Telegraph Alphabet No. 2 (ITA-22), the most common teleprinter code in use before ASCII (American Standard Code for Information Interchange) or ITA-5. Each character in the alphabet is represented by a series of five bits, sent over a communication channel such as a telegraph wire or radio signal by asynchronous serial communication.
- ITA-2 (International Telegraph Alphabet No.2) is a 5-bit character encoding system used in teleprinter (teletype) communications in the early 20th century.

Baudot code was used for teleprinter messages instead of morse code and allowed to encode 2^5=32 characters efficiently. Each character was preceded and followed by a bit to announce its start and end. Normal text consists of over 50 different characters (26 letters, 10 numbers and 10 punctuation marks and some control edges). In the ITA-2 standard, 5 bits are used to represent a character which means that only 32 different codes can be credited (2^5). 

## Gematria
Is the process of assigning a number to a name, word or phrase by giving each letter a numerical value. Gematria has its origin as a numerology based system where each Hebrew letter corresponds to a specific number ranging from 1 - 90. These numbers can be calculated to reveal inner meanings found in all sorts of Jewish literature.

In standard gematria each letter is given a numerical value between 1 and 400 with the final five letters given their own values ranging from 500 - 900. In traditional Hebrew &#1488; = 1, &#1489; = 2, &#1490; = 3 and so on. This system can also be applied and mapped to the Latin and standard English alphabets, doing so we get A = 1, B = 2, C = 3 and so on.

## Soundex
is a phonetic algorithm for indexing names by sound, mainly surnames (last names), rather than the way it is spelled. The goal was to find a surname even though it may have been recoded under various spellings. Only the First letter of the name is kept during the process from there any following vowels are dropped and only the remaining consonants are assigned values 1 - 6. The result creates a deterministic output for finding surnames.
Surnames that are spelled differently, like SMITH and SMYTH, are perfect examples for the Soundex system to tackle, both share the same code and are filed together. 
An example of how consonants are filed. 

| Letter | Code |
| ------ | ---- |
|b, f ,p, v | 1 | 
|c, g, j, k, q, s, x, z | 2 |
| d, t | 3 | 
|l | 4 | 
|m, n | 5 | 
|r | 6 |

# System Description 
The TAG-Engine is simple and follows a clean set of instructions
1. Input a word which is converted to uppercase
2. Each letter is assigned a position number (A=1, B=2, ..., Z=26) via `ord - 64`
3. Each number is padded with zeros(0) to 2 digits and compressed (concatenated) into one decimal string
4. The decimal string is treated as a single integer which is converted into binary
5. Binary string is padded to the nearest multiple of 5, then spilt into 5-bit chunks
6. Each chunk is converted into an integer(0-31) and mapped to a letter: 1-26 becomes A-Z, 27-31 becomes a-e, 0 becomes `_`
7. Non-alpha characters are filtered out
8. First three letters taken as the TRI-TAG, `.` Used as padding if fewer than three survive

The engine also supports a phrase/sentence mode, where a phrase, full sentence or paragraph can be entered as a single input. Each word is processed individually using the same algorithm and all QUIN-TAG outputs are returned on a single line, rather than requiring each word to be entered separately.

*The engine only takes letter inputs. Entering any numbers fo special characters will result in failure*

# Results
Below are a series of screenshots showing how words are converted during the algorithm. The First two words or the first two words every novice programmer will output. 'Hello' and 'World'. All words are capitalised upon being input to keep conversion clean and stable.
![hello](results/images/tages_image_1(hello).png)
*figure 1 showing the word 'Hello' being converted to WeZ and WeZKE'*

![world](results/images/tages_image_2(world).png)
*figure 2 showing the word 'World' being converted to BDe and BDecW'*

Not all words can be clearly converted into a complete TAG. Words that are 2 letters long such as 'at' and 'it'.
![at](results/images/tages_image_6(at).png)
*figure 3 showing the word 'at' being converted to CX. and CX...'*

![it](results/images/tages_image_7(it).png)
*figure 4 showing the word 'it' being converted to bX. and bX...'*

Adding one more letter will fix the problem with TRI-TAGs but QUIN-TAGs will continue to use *.* as a placeholder as they do not have enough letters to be fully converted.

Words that also follow similar spellings will also pose a chanllenge as they will produce the exact same tag if capped at TRI-TAGs. Take the famous there, their and they're trio. Only two of them there and their produce similar tags, however, producing a QUIN-TAG can help to resolve the problem

![there](results/images/tages_image_8(there).png)
*figure 5 showing the word 'there' being converted to Aaa and AaabB'*

![their](results/images/tages_image_9(their).png)
*figure 6 showing the word 'their' being converted to Aaa and AaaaG'*

Relying on QUIN-TAGs can also cause a similar problem with TRI-TAGs is the word is long enough. Take principal and principle. Both words share the exact spelling up until the final two letters and the only differences between them is the placement of the letter l and one word using a while the other uses e. Both words produce similar results and would need a tne-letter TAG to differentiate between the two.

![principal](results/images/tages_image_15(principal).png)
*figure 7 showing the word 'principal' being converted to DOV and DOVbQ'*

![principle](results/images/tages_image_16(principle).png)
*figure 8 showing the word 'principle' being converted to DOV and DOVbQ'*

For both words to truly have a unique TAG, principal would need to be *DOVbQYDXSb* and principle would need to be *DOVbQYDXSc*

[Results Table](results/results_table.md)

# Discussion 
## Completionn
As previously mentioned the algorithm does have its limits. If a word is 2 letters long, it will not produce a full TRI-TAG and a full QUIN-TAG. If a word is 3 letters long, it can produce a full TRI-TAG but not a full QUIN-TAG.

## Collisions
Using figure 5, figure 6, figure 7 and figure 8, we see that the system is not perfect and has its faults. Between all of these examples, one key detail are the similar spellings. All words contain the exact same amount of letters with only one letter being the major difference in spelling. Because of that we have similar letter to number conversion, similar binary strings and similar chunk generation. 

Collisions will always be a major factor for the algorithm, especially with TRI-TAGs. Using the mathematical concept of permutations, an ordered arrangement of all or part of a set of objects, where the specific order of selection matters, we can only achieve a total of 15,600 permutations. Alternatively if we use QUIN-TAGs we get a total of 7,893,600 permutations. With an estimated 1,000,000 (1 million) words in the English language, we can clearly see how limited the TRI-TAGs can be when expressing words through the algorithm. 

## lossy encoding
The algorithm as a whole is a lossy encoding system, meaning that the original information, input word, is lost during the process. It occurs during the process of converting the binary string into 5-bit chunks. After that process is complete the original informatoin is forever lost and can never be recovered. This means that unless a user has the original input, it can never be decoded.

## Case Senitivity Neutralisation
All words entered into the algorithm are automatically capitalised as a safeguard. By making each input capitalised it reduces or neutralises the need for complex functions to handle both lowercase and capitalised letters. Since all English words make use of the 26 letters of the alphabet it would make no difference to use lowercase of capital letters. Aa, Bb, Cc would still be mapped to 1, 2 and 3 respectively.

Each word is set to one standard making processing easier and faster. The output of the TAGs are also capitalised to keep symmetry throughout the system and to make the output more readable as each capital letter has distinct shape that is recognised when viewing on a screen. On the contrast, TAGs can have lowercase letters, however. in this case they are used to extend the functionality of the algorithm. 

If the alogirthm had only used the capitalised letters, it would have a limited output for longer words as it would be limited to the 26 letters of the alphabet. By introducing lowercase letters, we extend the range from 26 to 52 allowing us to print more specialised TAGs when dealing with longer words.

## Related Words
The TAGES algorithm has some similarities and differences with a number of systems.

UUID is asystem to generate a pusedo-random code that can be appiled to any item. Version 3 and Version 5 of UUID were built with security and encryption purposes in mind. TAGES differs by being deterministic and was built around the theme of generating labels for items and assets. 

Like Gematria it maps letters to numbers, however, it goes further. Instead of adding those numbers, it converts those numbers to binary then combine those binary convertions into a singular binary string which later gets broken into 5-bit chunks. 

Which takes inspiration from Baudot code' 5-bit processing by processing. Prior to the final TAG output, the algorithm displays the binary string split into 5 distinct chunks. These results are not human readable and thus required additional mapping steps to produce the compact readable TAGs the algorithm generates.

Finally like Soundex, it reduces te original input to a compact code. Where they differ is that Soundex preserves phonetic meaning, whereas TAGES discards all meaning intentionally. 

# Conclusion
The TAG-Engine System (TAGES) was designed to produce a derterministic compact identifier for use in fictional universe timeline naming. The algorithm successfully converts any word into a TRI-TAG or QUIN-TAG through a series of ASCII, binary and 5-bit chunk conversion. Results show that while the system functions as intended, it has its faults such as collisions at the TRI-TAG level and lossey encoding. Despite its limits TAGES achieves its core goal of generating standardised labels.

# References
## The Transformers Multiverse
- Transformers Multiverse. *How the Names of Transformers Universes Work*. Quora. https://transformersmultiverse.quora.com/How-the-names-of-Transformers-Universes-work
- Transformers Multiverse. *How Does the Transformers Multiverse Work*. Quora. https://transformersmultiverse.quora.com/How-does-the-Transformers-Multiverse-work
- TFWiki. *Universal Stream*. https://tfwiki.net/wiki/Universal_stream
- TFWiki. *Primax 984.17 Alpha*. https://tfwiki.net/wiki/Primax_984.17_Alpha

## Deterministic Identifier Schemas
- RudderStack. *Deterministic vs Probabilistic*. https://www.rudderstack.com/blog/deterministic-vs-probabilistic/
- AdMonsters. *What Are Deterministic and Probabilistic IDs?*. https://www.admonsters.com/ad-ops-decoder-what-are-deterministic-and-probabilistic-ids/
- ScienceDirect. *Deterministic Identifier Research*. https://www.sciencedirect.com/science/article/abs/pii/S0952197622006315

## Universally Unique Identifier (UUID)
- IETF. *RFC 9562 — UUID Version 5*. https://www.rfc-editor.org/rfc/rfc9562.html#name-uuid-version-5
- Kinto Technologies. *What Are UUIDs and Which Version Should You Use?*. https://blog.kinto-technologies.com/posts/2025-02-12-WhatAreUUIDsAndWhichVersionShouldYouUse/
- Wikipedia. *MD5*. https://en.wikipedia.org/wiki/MD5
- GeeksforGeeks. *What Is the MD5 Algorithm?*. https://www.geeksforgeeks.org/computer-networks/what-is-the-md5-algorithm/
- Wikipedia. *SHA-1*. https://en.wikipedia.org/wiki/SHA-1
- GeeksforGeeks. *SHA-1 Hash in Java*. https://www.geeksforgeeks.org/java/sha-1-hash-in-java/

## Baudot Code
- Wikipedia. *Baudot Code*. https://en.wikipedia.org/wiki/Baudot_code
- Crypto Museum. *ITA-2 Reference*. https://www.cryptomuseum.com/ref/ita2/index.htm
- Stanford University. *Baudot Code — Colossus Project*. https://cs.stanford.edu/people/eroberts/courses/soco/projects/2008-09/colossus/baudot.html
- University of New Brunswick. *Baudot Code Reference*. https://www.ece.unb.ca/tervo/ee4253/baudot.shtml
- Wikipedia. *Telegraph Code*. https://en.wikipedia.org/wiki/Telegraph_code

## Gematria
- Wikipedia. *Gematria*. https://en.wikipedia.org/wiki/Gematria
- Computer Hope. *Gematria Definition*. https://www.computerhope.com/jargon/g/gematria.htm
- Aish. *What Is Gematria?*. https://aish.com/what-is-gematria/

## Soundex
- Wikipedia. *Soundex*. https://en.wikipedia.org/wiki/Soundex
- U.S. National Archives. *Soundex System*. https://www.archives.gov/research/census/soundex
