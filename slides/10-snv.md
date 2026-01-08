---
---

# SNV Data

TopMED Freeze 10 SNV data live on production site

- [Region](https://bravo.sph.umich.edu/region.html?chrom=11&start=5225000&stop=5229000)
- [Gene](https://bravo.sph.umich.edu/gene.html?id=HBB)
- [Variant](https://bravo.sph.umich.edu/variant.html?id=rs193922562)

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

## UI: Vue Components.

Modulararity allows UI components to be developed independently.

```html
<template>
  <div class="child-component">
    <svg id="bp-coord-bar" 
      style="display: block;" height="100px" width="100%" 
      viewBox="0 0 1000 100" preserveAspectRatio="none">
      <g id="x-axis-container"></g>
    </svg>
</div>
</template>
<script>
  import * as d3 from "d3"
  export default { name: "BpCoordBar" }
</script>
```
