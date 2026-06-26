# Noto CJK Font

This package contains several pre-built CJK fonts. You can use this font to display the common Traditional Chinese, Simplified Chinese, Japanese and now Korean characters with only one font file. This is particularly useful for Kobo e-readers because its font fallback mechanism is not very good.

Here is the default fonts in Kobo Libre Color. You can see they have various issues.

| 文鼎明體 | 築紫明朝 | Bitter |
|-|-|-|
| ![文鼎明體](docs/文鼎明體.JPEG) | ![築紫明朝](docs/築紫明朝.JPEG) | ![Bitter](docs/Bitter.JPEG) |
| The apostrophe is full-sized. It makes pure English rendering ugly. | Some Chinese words disappeared completely. | Some Chinese words are missing and leave empty space. |

Here is the Noto Sans / Serif fonts produced by this script. You can see the display is perfect.

| Noto Sans CJK (Light) | Noto Serif CJK (Light) |
|-|-|
| ![Noto Sans](docs/NotoSans.JPEG) | ![Noto Serif](docs/NotoSerif.JPEG) |

Any missing characters can be reported to us ;-)

# Font Installation

Download the pre-built CJK font [`NotoSerifCJK-Light.ttf`](NotoSerifCJK-Light.ttf) and install the font.

If you are using Kobo, you can follow this guide to install the font: https://help.kobo.com/hc/en-us/articles/13009477876631-Load-fonts-onto-your-Kobo-eReader

# Script Usage

If you want to produce the CJK font file yourself, you can use the script `merge-cjk-font.py`.

You can install the requirements by running `pip install -r requirements.txt` first.

Then you can run the script to produce the CJK font file that contains the common Chinese, Japanese, and Korean characters.

This is an example of how to run the script:

```
run() {
    local serif_or_sans="$1"
    local weight="$2"

    local dir="${serif_or_sans}-${weight}"
    merge-cjk-font.py \
        --latin "${dir}/Noto${serif_or_sans}-${weight}.ttf" \
        --zh-cn "${dir}/Noto${serif_or_sans}SC-${weight}.ttf" \
        --zh-tw "${dir}/Noto${serif_or_sans}TC-${weight}.ttf" \
        --ja "${dir}/Noto${serif_or_sans}JP-${weight}.ttf" \
        --add-latin1 \
        --add-general-punct \
        --general-punct-owner latin \
        --add-cjk-punct \
        --add-jp-syllabaries \
        --add-halfwidth \
        --add-han-basic \
        --drop-tables vhea vmtx \
        --out "Noto${serif_or_sans}CJK-${weight}.ttf" \
        --out-name "Noto ${serif_or_sans} CJK" \
        --out-subfamily "${weight}"
}

# run 'Serif' 'Light'
# run 'Serif' 'Regular'
# run 'Sans' 'Light'
# run 'Sans' 'Regular'
```


# For korean : 

```
python merge-cjk-font.py `
  --latin NotoSerif-Regular.ttf `
  --zh-cn NotoSerifKR-Regular.ttf `
  --add-latin1 --add-general-punct --general-punct-owner latin `
  --add-cjk-punct --add-jp-syllabaries --add-halfwidth --add-han-basic --add-hangul `
  --drop-tables vhea vmtx `
  --out KoboNotoSerif-Regular.ttf `
  --out-name "Kobo Noto Serif" --out-subfamily "Regular"
```

`--general-punct-owner` can redirect the general punctuation block (U+2000–U+206F)
to a specific language tag (e.g., `latin` to keep curly quotes from a Latin font so that it doesn't occupy additional space). If omitted, the normal prefer order is used.
