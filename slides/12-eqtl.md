---
---

# eQTL Data

Freeze 1 eQTL data live on production site. Based on TopMED freeze 8 data.
![](assets/bravo_eqtl_screen.png)

## eQTL Views

- [Gene](https://bravo.sph.umich.edu/gene.html?id=TNF#eqtl)
- [Region](https://bravo.sph.umich.edu/region.html?variant_type=snv&chrom=11&start=5225464&stop=5229395#eqtl)
- [Variant](https://bravo.sph.umich.edu/variant.html?id=6-31597981-T-G)

## Data Processed via Nextflow

Framework standard modular composition.

```nf
workflow susie_eqtl {
  analysis_type = "susie"
  susie_tsv     = channel.fromPath("${params.susie_eqtl_glob}")
  susie_headers = channel.of(params.susie_fields).collect()
  fields        = params.susie_fields
  types         = params.susie_types

  validate_header(susie_tsv, susie_headers)
  munge_files(susie_tsv, analysis_type)
  merge_files(munge_files.out.collect(), 
              analysis_type, fields, types)
}
```

## Visualization in a Vue Component.

Framework standard modular composition.

```html
<template>
<div class="child-component">
  <div ref="eqtltable" class="table-sm"></div>
</div>
</template>

<script>
import Tabulator from 'tabulator-tables'
export default {
 name: "EqtlSusieTable"
}
</script>
```
