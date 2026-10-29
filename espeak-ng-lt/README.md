# Sources of `lt_dict`

`dictsource/` holds the complete source of the `lt_dict` in the release:

- `lt_rules`, `lt_emoji`: unchanged eSpeak NG files (see [../THIRD_PARTY.md](../THIRD_PARTY.md)).
- `lt_list`: eSpeak NG's list, followed by 189,209 lines `word $N` (primary stress on syllable
  N), with the attribution in a comment above them.

`$N` counts syllables the way eSpeak NG does for Lithuanian. eSpeak NG treats the hard l as
syllabic in many words ("labai" → `l'abai` without the list) and counts it, so N was taken from
eSpeak NG's own phoneme output for every word.

To build it yourself, put the three files into an eSpeak NG source tree's `dictsource/` and
compile the Lithuanian dictionary with eSpeak NG's dictionary compiler (`espeak-ng --compile=lt`
run in that folder, or the CMake `data` target). We compiled it with libespeak-ng's
`espeak_ng_CompileDictionary`; against the eSpeak NG data used by sherpa-onnx (as in SherpaTTS
3.4) it gives `lt_dict` with md5 `1f93dc81303ee88017998f029468beb1`.
