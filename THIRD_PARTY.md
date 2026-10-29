# Third-party material

## The voice

`lt_LT-ingute-medium.onnx` is the Ingutė voice from the Piper voice catalogue
(https://huggingface.co/rhasspy/piper-voices, `lt/lt_LT/ingute/medium`) with sherpa-onnx metadata
added (`model_type`, `comment`, `language`, `voice`, `has_espeak`, `n_speakers`, `sample_rate`);
the network weights are unchanged. `tokens.txt` is generated from the voice's
`phoneme_id_map`: keys longer than one code point are left out (sherpa-onnx cannot read them and
eSpeak NG never produces them), and `ʂ` gets the id of `s`.

Licence: NewGenLTU Open RAIL-D License 1.0, full text in [LICENSE-VOICE](LICENSE-VOICE)
(https://sitti.vdu.lt/newgenltu-openrail-d-license/). Voice repository:
https://huggingface.co/RobertasTa/lt_LT-ingute-medium

## eSpeak NG data (`lt_dict`, `espeak-ng-lt/`)

`lt_dict` is compiled with eSpeak NG's dictionary compiler from the files in
`espeak-ng-lt/dictsource/`:

- `lt_rules`, the first part of `lt_list`, `lt_emoji`: eSpeak NG
  (https://github.com/espeak-ng/espeak-ng), GPL-3.0. `lt_rules` and `lt_list` as in eSpeak NG
  master; `lt_emoji` as in the eSpeak NG fork used by sherpa-onnx
  (https://github.com/csukuangfj/espeak-ng), so that the unchanged files compile to the same
  `lt_dict` that SherpaTTS 3.4 ships (md5 `5426503daf0a29836d0f168d38b38581`).
- The added block at the end of `lt_list` (189,209 lines `word $N`): the stressed syllable of
  each word form, taken from `lt_kirciai.tsv` as shipped in OHF-Voice/piper1-gpl
  (`src/piper/lithuanian/`, GPL-3.0), which is built from two works licensed under the
  Creative Commons Attribution 4.0 International licence:
  - LIEPA corpus annotation, Vilnius University:
    https://huggingface.co/datasets/meldynamics/liepa-tts
  - g2p-lt-lexicon, Arūnas Smaliukas: https://github.com/svogunas/g2p-lt-lexicon

The resulting `lt_dict` is distributed under GPL-3.0 with these sources.

## Not included

SherpaTTS (https://github.com/woheller69/ttsengine, GPL-3.0) is a separate app and is not part
of this package. Install it from F-Droid.
