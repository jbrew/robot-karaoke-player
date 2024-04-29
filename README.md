## Robot karaoke player

Web player for karaoke songs with procedurally generated replacement lyrics.

## Robot karaoke data format

Files are `.jsonl` ("JSON lines") which means newline-separated json objects. Spec: https://jsonlines.org/

The first line of the file is metadata about the song:

title: string
artist: string
url: string

All remaining lines of the file represent lines of lyrics:

originalText: string, The lyrics of the original song.
originalTokens: Token[], Text with same number of syllables as the original text.
replacementText: string, same as originalText
replacementTokens: Token[], same as originalTokens
replacementSrc: ?string, Location of the replacement text's associated image, if any.
timestamps: ?number[], Syllable onset times in seconds, relative to the start of the song. If the whole line appears at once, you can use its first timestamp. If this field is null, we need user input to advance the lines.

Token:
text: string,
vowels: string[],
phones: ?string[],
stresses: string[],