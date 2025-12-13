This workflow is to use vcs to generate thumbnail previews.

'''
brew install vcs
'''

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
