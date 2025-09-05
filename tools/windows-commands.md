Delete all files that have the suffix `.srt` except by `*_en.srt`.
```bash
find . -type f -name "*.srt" ! -name "*_en.srt" -exec rm {} \;
```