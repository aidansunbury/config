# config
Starter config files to easily add to new projects

## Biome (version 1.9.4)
```bash
curl -o biome.json https://raw.githubusercontent.com/aidansunbury/config/main/biome.json
echo "Added biome.json from config file at https://github.com/aidansunbury/config"
bun add --dev --exact @biomejs/biome@1.9.4
echo "Be sure to add the following script to your package.json"
echo '"biome": "bunx biome check --write --unsafe src/*",'
```