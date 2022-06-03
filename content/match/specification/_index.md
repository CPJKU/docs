---
# Title, summary, and page position.
linktitle: Format Specification
summary: specification of the match file format.
weight: 3

# Page metadata.
title: Match File Format
date: "2018-09-09T00:00:00Z"
type: book  # Do not modify.
---


## Global Information Lines



| **Syntax**                                | **Value** **type**      | **Mandatory** | **Description**                                              |
| ----------------------------------------- | ----------------------- | ------------- | ------------------------------------------------------------ |
| **info(matchFileVersion,****value****).** | **string**              |               | **Matchfile version (current 1.0.0 previous 5.0, see version changes)** |
| **info(piece,****value****).**            | **string**              |               | **Piece name or opus number**                                |
| **info(scoreFileName,****value****).**    | **string**              |               | **Corresponding score file name (e.g. musicxml)**            |
| **info(scoreFilePath,****value****).**    | **string**              |               | **Corresponding score file path**                            |
| **info(midiFileName,****value****).**     | **string**              |               | **Corresponding MIDIfile name**                              |
| **info(midiFilePath,****value****).**     | **string**              |               | **Corresponding MIDI file path**                             |
| **info(audioFileName,****value****).**    | **string**              |               | **Corresponding audio file name**                            |
| **info(audioFilePath,****value****).**    | **string**              |               | **Corresponding audio file path**                            |
| **info(audioFirstNote,****value****).**   | **float**               |               | **Time of first note onset in audio file**                   |
| **info(audioLastNote,****value****).**    | **float**               |               | **Time of last note onset in audio file**                    |
| **info(performer,****value****).**        | **string**              |               | **Performer name**                                           |
| **info(composer,****value****).**         | **string**              |               | **Composer name**                                            |
| **info(midiClockUnits,****value****).**   | **integer**             |               | **MIDI Clock Units (MIDI parts per quarter)**                |
| **info(midiClockRate,****value****).**    | **integer**             |               | **MIDI Clock Rate (Microseconds per quarter)**               |
| **info(keySignature,****value****).**     | **[string]**            |               | **deprecated** **(first) Key signature (see score properties)** |
| **info(timeSignature,****value****).**    | **[integer / integer]** |               | **deprecated** **(first) Time signature (see score properties)** |
| **info(beatSubdivision,****value****).**  | **[int]**               |               | **deprecated** **Beat subdivision (see score properties)**   |
| **info(tempoIndication,****value****).**  | **[string]**            |               | **deprecated** **Tempo directions (see score properties)**   |
| **info(approximateTempo,****value****).** | **float**               |               | **Approximate tempo**                                        |
| **info(subtitle,****value****).**         | **string**              |               | **Subtitles**                                                |

## Score Property Lines

### Time Signature:

`scoreprop(timeSignature,TimeSigValue,Measure:Beat,Offset,Duration,OnsetInBeats).`

### Key Signature:

`scoreprop(keySignature,KeySigValue,Measure:Beat,Offset,Duration,OnsetInBeats).`

### Beat Subdivision:

 `scoreprop(beatSubDivision,BeatSubValue,Measure:Beat,Offset,Duration,OnsetInBeats).`

### Directions:

`scoreprop(directions,DirectionsValue,Measure:Beat,Offset,Duration,OnsetInBeats).`



| **Value name**      | **Value type**        | **Description**                                              |
| ------------------- | --------------------- | ------------------------------------------------------------ |
| **Measure**         | **integer**           | **measure number (starting at 1, 0 for anacrusis) of the score position** |
| **Beat**            | **integer**           | **integer beat number (starting at 1) of the score position** |
| **Offset**          | **Integer / integer** | **offset of the score position****from beat position (in symbolic duration; fraction of whole notes)** |
| **OnsetInBeats**    | **float**             | **score position in contiguous beats (beat 0 = start of measure 1, beat unit = time signature denominator)** |
| **TimeSigValue**    | **integer / integer** | **Time signature**                                           |
| **KeySigValue**     |                       | **Key signature**                                            |
| **BeatSubValue**    | **Integer**           | **?**                                                        |
| **DirectionsValue** | **[string]**          | **A list of performance directions**                         |



## Section Lines



### Section in the score with reference positions in the underlying (non-unfolded) score:

`section(StartInBeatsUnfolded,EndInBeatsUnfolded, StartInBeatsOriginal, EndInBeatsOriginal, RepeatEndType).`



Possible values:

| **Value name**           | **Value type** | **Description**                                              |
| ------------------------ | -------------- | ------------------------------------------------------------ |
| **StartInBeatsUnfolded** | **float**      | **Start of the segment in beats in unfolded score time**     |
| **EndInBeatsUnfolded**   | **float**      | **End of the segment in beats in the unfolded score time**   |
| **StartInBeatsOriginal** | **float**      | **Start of the segment in beats in the original score**      |
| **EndInBeatsOriginal**   | **float**      | **End of the segment in beats in the original score**        |
| **RepeatEndType**        | **[string]**   | **optional: list of type of the end of segment, e.g. “fine” “repeat left”, “volta end”, etc.** |

## Match Lines

### Beat, downbeat, or any score position annotation between performance and score:

`stime(Measure:Beat,Offset,OnsetInBeats,AnnotationType)-ptime(Onsets).`

| **Value name**     | **Value type**        | **Description**                                              |
| ------------------ | --------------------- | ------------------------------------------------------------ |
| **Measure**        | **integer**           | **measure number (starting at 1, 0 for anacrusis) of the score position** |
| **Beat**           | **integer**           | **integer beat number (starting at 1) of the score position** |
| **Offset**         | **Integer / integer** | **offset of the score position****from beat position (in symbolic duration; fraction of whole notes)** |
| **OnsetInBeats**   | **float**             | **score position in contiguous beats (beat 0 = start of measure 1, beat unit = time signature denominator)** |
| **AnnotationType** | **[string]**          | **Optional: list of types of annotation, e.g. “beat”, “measure”, or “downbeat”** |
| **Onsets**         | **[integer]**         | **Array of at least one time in parts/ticks of the performance annotation corresponding to the score position** |



**Notes in the performance:**

`note(ID,MIDIpitch,Onset,Offset,Velocity).`



| **Value name**     | **Value type** | **Description**                                              |
| ------------------ | -------------- | ------------------------------------------------------------ |
| **ID**             | **integer**    | **Note identifier**                                          |
| **MIDIpitch**      | **integer**    | **Pitch 0-127**                                              |
| **Onset**          | **integer**    | **Time in parts/ticks of the note on message**               |
| **Offset**         | **integer**    | **Time in parts/ticks of the note off message**              |
| **adjustedOffset** | **integer**    | **deprecated** **Sounding note off when adjusted by sustain pedal information (see pedal lines)** |
| **Velocity**       | **integer**    | **Note on velocity 0-127**                                   |



### Notes in the score

`snote(Anchor,[NoteName,Modifier],Octave,Measure:Beat,Offset,Duration,OnsetInBeats,OffsetInBeats,ScoreAttributesList).`



| **Value name**          | **Value type**        | **Description**                                              |
| ----------------------- | --------------------- | ------------------------------------------------------------ |
| **Anchor**              | **string**            | **Note identifier (we should specifically reserve “-<number>” at the end of the anchor as “repetition”)** |
| **NoteName**            | **string**            | **Pitch class name in [C, D, E, F, G, A, B]**                |
| **Modifier**            | **string**            | **pitch modifier in [“”, n, b, #, bb, x]**                   |
| **Octave**              | **integer**           | **octave number (scientific notation, middle C is in octave 4)** |
| **Measure**             | **integer**           | **measure number (starting at 1, 0 for anacrusis)**          |
| **Beat**                | **integer**           | **integer beat number of note onset (starting at 1)**        |
| **Offset**              | **integer / integer** | **offset from beat position (in symbolic duration; fraction of whole notes)** |
| **OnsetInBeats**        | **float**             | **onset position in contiguous beats (beat 0 = start of measure 1, beat unit = time signature denominator)** |
| **DurationInBeats**     | **float**             | **duration in beats**                                        |
| **ScoreAttributesList** | **[string]**          | **note attributes (“grace”, “appoggiatura”, etc.)**          |



### score note matched to a performed note:

`snote( _ , … , _ )-note( _ , … , _ ).`

`snote(Anchor,NoteName,Modifier],Octave,Measure:Beat,Offset,Duration,OnsetInBeats,OffsetInBeats,ScoreAttributesList)-note(ID,MIDIpitch,Onset,Offset,Velocity).`



| **Value name**          | **Value type**        | **Description**                                              |
| ----------------------- | --------------------- | ------------------------------------------------------------ |
| **Anchor**              | **string**            | **Note identifier (we should specifically reserve “-<number>” at the end of the anchor as “repetition”)** |
| **NoteName**            | **string**            | **Pitch class name in [C, D, E, F, G, A, B]**                |
| **Modifier**            | **string**            | **pitch modifier in [“”, n, b, #, bb, x]**                   |
| **Octave**              | **integer**           | **octave number (scientific notation, middle C is in octave 4)** |
| **Measure**             | **integer**           | **measure number (starting at 1, 0 for anacrusis)**          |
| **Beat**                | **integer**           | **integer beat number of note onset (starting at 1)**        |
| **Offset**              | **integer / integer** | **offset from beat position (in symbolic duration; fraction of whole notes)** |
| **OnsetInBeats**        | **float**             | **onset position in contiguous beats (beat 0 = start of measure 1, beat unit = time signature denominator)** |
| **DurationInBeats**     | **float**             | **duration in beats**                                        |
| **ScoreAttributesList** | **[string]**          | **note attributes (“grace”, “appoggiatura”, etc.)**          |
| **ID**                  | **integer**           | **Note identifier**                                          |
| **MIDIpitch**           | **integer**           | **Pitch 0-127**                                              |
| **Onset**               | **integer**           | **Time in parts/ticks of the note on message**               |
| **Offset**              | **integer**           | **Time in parts/ticks of the note off message**              |
| **adjustedOffset**      | **integer**           | **deprecated** **Sounding note off when adjusted by sustain pedal information (see pedal lines)** |
| **Velocity**            | **integer**           | **Note on velocity 0-127**                                   |



### Omitted score note 

Score notes that were omitted in the performance:

`snote( _ , … , _ )-deletion.`



### Inserted Performed note:

Performed notes that are not found in the score:

`insertion-note( _ , … , _ ).`





## Pedal Lines

Pedal lines represent MIDI cc 64 (sustain pedal) messages in the performance MIDI file.



**Pedal line:**

`sustain(Time,Value).`



| **Value name** | **Value type** | **Description**                              |
| -------------- | -------------- | -------------------------------------------- |
| **Time**       | **integer**    | **Time in parts/ticks of the pedal message** |
| **Value**      | **integer**    | **Sustain pedal value 0-127**                |
