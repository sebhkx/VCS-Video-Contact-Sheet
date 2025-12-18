# use vcs to generate thumbnail previews. <br>
Workflow app: change to pass input as arguments!
```
brew install vcs
```
* ffmpeg
* ffprobe
```
export PATH="/opt/homebrew/bin:/usr/bin:/bin:/usr/sbin:/sbin"
export TERM=xterm-256color
exec </dev/null

for input in "$@"; do
  dir="${input:h}"
  file="${input:t}"

  if [[ "$file" =~ ([A-Za-z]+-[0-9]+) ]]; then
    out="$dir/${match[1]}_s.jpg"
    vcs -n 30 --disable timestamps -o "$out" "$input"
  else
    osascript -e "display alert \"No ID found\" message \"Filename does not contain pattern ABC-123\""
  fi
done

magick "$out" -gravity south -chop 0x28 +repage "$out"

afplay /System/Library/Sounds/Glass.aiff
``'

# reportlab & PyPDF2
1. Generate blank A4 pdf
2. Overlay (smaller pdf) on A4 (default coordinate 0,0 is bottom left) -- to work on top left alignment
