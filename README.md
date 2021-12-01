# Rebuild Site

## Install `vangen`

```bash
go install 4d63.com/vangen@latest
```

## Update `vangen.json` to include new import / repository path

```json
{
    "prefix": "newpkg",
    "url": "https://github.com/Contrast-Security-Inc/newpkg"
}
```

## Execute `vangen`

`vangen -out .`
