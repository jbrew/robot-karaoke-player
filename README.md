## Robot karaoke player

Web player for karaoke songs with procedurally generated replacement lyrics.

## Data format

Files are `.jsonl` ("JSON lines") which means newline-separated json objects. Spec: https://jsonlines.org/

The first line of the file is metadata about the song:

```
{
  title: string,
  artist: string,
  url: string
}
```

All remaining lines of the file represent lines of lyrics:

```
{
  originalText: string
  replacementText: string
  replacementSrc: ?string
  timestamps: ?number[]
}
```

Explanations:
`originalText`: The lyrics of the original song.
`replacementText`: Text with same number of syllables as the original text.
`replacementSrc`: Location of the replacement text's associated image, if any.
`timestamps`: Syllable onset times in seconds, relative to the start of the song. If the whole line appears at once, you can use its first timestamp. If this field is null, we need user input to advance the lines.

Note: To precisely highlight text within the line, we need to know how the vowels map onto the text. I've left that out of the schema for simplicity, but may add it later.

## Example

```
{"title":"Do You Believe In Magic","artist":"The Lovin' Spoonful","url":"https://www.youtube.com/watch?v=CyB4lDKAjoM"}
{"originalText":"Do you believe in magic","replacementText":"Tomb of the Spirit Dragon","replacementSrc":"https://gatherer.wizards.com/Handlers/Image.ashx?multiverseid=386700&type=card", timestamps: [11.488,11.641,11.923,12.084,12.368,12.836,13.254]}
{"originalText":"in a young girl's heart?","replacementText":"Gilded Assault Cart","replacementSrc":"https://gatherer.wizards.com/Handlers/Image.ashx?multiverseid=506932&type=card", timestamps: [14.322,14.597,14.746,14.993,15.442]}
...
```
