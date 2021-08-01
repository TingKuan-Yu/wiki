# reference doc
- https://docs.microsoft.com/en-us/cli/azure/artifacts/universal?view=azure-cli-latest

# az artificates
- download artifact-version.json of the latest version
```
tingkuanyu@TonyYuLinux1:/media/tingkuanyu/EXT4/c1/serverbuild/test$ az artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "c1-11-main-images" --name "c1-11-developer-combo" --version "*" --file-filter artifact-version.json   --path .
{- Downloading ..
  "Description": "r1.0.c8_00010.4 Wiki Link: https://dev.azure.com/E-OS/eos/_wiki/wikis/Integration-Builds?wikiVersion=GBmaster&pagePath=/Integration/c1-11-developer-c1-11-main-images/2021.717.3",
  "ManifestId": "CDB428703F3ACD98E64BC023437860BF311D21F707356A9DB83A71121B83267202",
  "SuperRootId": "666433EE612475EBCD2B656B425099F0570E965B48E3619BC7EEB7D29C067DD402",
  "Version": "2021.717.3"
}
tingkuanyu@TonyYuLinux1:/media/tingkuanyu/EXT4/c1/serverbuild/test$ ls
artifact-version.json
tingkuanyu@TonyYuLinux1:/media/tingkuanyu/EXT4/c1/serverbuild/test$ cat artifact-version.json 
{
  "name": "combo",
  "version": "2021.717.3"
}
```