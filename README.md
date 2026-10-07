
# CBIA Developer Tools Compatibility Matrix Project

This page serves to publish Project updates and Technical aspects for Catalyst funded proposal [CBIA - Add Developer Tool Compatibility Matrix to Cardano Developers Portal](https://projectcatalyst.io/funds/11/cardano-open-developers/cbia-add-developer-tool-compatibility-matrix-to-cardano-developers-portal).

## Milestone #1 - “Ms1-Data”

### Stakeholder Updates

Regarding the Stakeholders side of this milestone, we confirm we are now in contact with the Cardano Foundation Dev Portal maintainers, having chatted with [Tommy](https://x.com/adatainment) (CF Community Team) and met with [Bora Oben](https://www.linkedin.com/in/boraoben) (Developer Advocate), who is in charge of overseeing changes to this portal.

We have also engaged with some Dev Portal tooling authors via a [GitHub issue on the portal’s repository](https://github.com/cardano-foundation/developer-portal/issues/1091) and gathered initial [indication of the compatibility of their tool with others](https://docs.google.com/spreadsheets/d/1IJ2LmhQpYqyL4M6hlg0YyVQDlqdqHy4VA54EehP0MLQ) from some CBIA members.

![Call between CBIA and Cardano Foundation](/readme_static/CBIAxCF_call.png)

### Technical Updates

Regarding the Technical side of this milestone, we have established a Data structure to enable the portal to gather the relationships and compatibility between different tools.

The data file located at `developer-portal/src/data/builder-tools.js` should be extended.

```js 
// Original data structure
{
    "title": "cardanocli-js",
    "description": "A library that wraps the cardano-cli in JavaScript.",
    "preview": "require('./builder-tools/cardanocli-js.png')",
    "website": "https://github.com/Berry-Pool/cardanocli-js",
    "getstarted": "/docs/get-started/cardanocli-js",
    "tags": ["javascript", "sdk"],
},
```

It will have a `releases` section, including `version`, `latest`, `dependencies` and `traits`.

```js
// Extended data structure
{
  "title": "cardanocli-js",
  "description": "A library that wraps the cardano-cli in JavaScript.",
  "preview": "require('./builder-tools/cardanocli-js.png')",
  "website": "https://github.com/Berry-Pool/cardanocli-js",
  "getstarted": "/docs/get-started/cardanocli-js",
  "tags": ["javascript", "sdk"],
  "releases": [
    {
      "version": "3.1.2",
      "latest": true,
      "dependencies": ["cardano-node"],
      "traits": ["babbage", "alonzo", "cip31", "cip32"]
    },
    {
      "version": "3.1.1",
      "dependencies": ["cardano-node"],
      "traits": ["alonzo"]
    }
  ]
}
```

To prove this, we have built the technical changes necessary to the Developer Portal, achieving an initial version of the code that will display these relationships and compatibility within the portal.

The repository can be found at https://github.com/Tanglius/cardano_matrix (its readme includes instructions to run it locally).

Here are a few screenshots exploring future use cases:
![Ms1-ScreenShot01.png](/readme_static/Ms1-ScreenShot01.png)
![Ms1-ScreenShot02.png](/readme_static/Ms1-ScreenShot02.png)
![Ms1-ScreenShot03.png](/readme_static/Ms1-ScreenShot03.png)
![Ms1-ScreenShot04.png](/readme_static/Ms1-ScreenShot04.png)


## Milestone #2 - “Ms2-Viz”

### Evidence of milestone completion

- Dependency Graph [running website here](https://45b.io/cbia-infra-tools/tools-rels-compat/). We highlight some features:

  - Button on the /tools/ landing page.

![Ms2-ScreenShot01.png](/readme_static/Ms2-ScreenShot01.png)

  - Visualization /tools-rels-compat/ on first load.

![Ms2-ScreenShot02.png](/readme_static/Ms2-ScreenShot02.png)

  - `Expand all` show dependents for bech32, flagging some incompatibility in red.

![Ms2-ScreenShot03.png](/readme_static/Ms2-ScreenShot03.png)

  - Scrolling down shows other `Top-level` tools, highlighting compatibility in green.

![Ms2-ScreenShot04.png](/readme_static/Ms2-ScreenShot04.png)

  - Toggling to `All tools` and `Collapse all` lists all 84 tools on the platform.

![Ms2-ScreenShot05.png](/readme_static/Ms2-ScreenShot05.png)

  - `Ctrl+Click` on a particular tool shows all dependents; Hovering over one shows info about its maker and description.

![Ms2-ScreenShot06.png](/readme_static/Ms2-ScreenShot06.png)

  - Toggling to `Dependencies` we can see all the tools that depend on a particular 'root' tool (Atlas in this case).

![Ms2-ScreenShot07.png](/readme_static/Ms2-ScreenShot07.png)

  - Clicking a particular Category allows us to see dependencies for example all the 'Smart Contracts' items.

![Ms2-ScreenShot08.png](/readme_static/Ms2-ScreenShot08.png)

  - `Ctrl+Click` allows us to add categories one by one.

![Ms2-ScreenShot09.png](/readme_static/Ms2-ScreenShot09.png)




- Dependency Graph **source code**, was committed to the main repo in two commits:

  - [First commit](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/commit/1708fd61b47fb762ab222781ed2405fcb1ac46b8) importing the visualization tree, data and data-enriching script which we developed as a standalone

  - [Second commit](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/commit/ea1ee6d3cc3f73dee1e664a5d55f27972ff20766) incorporating it into the existing portal pages and style

  - The current visualization is the result of greatly extending the data by using the formats outlined above, in Milestone #1.
    - Here are the [Original](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/blob/cbia-rels-compat/src/data/builder-tools/tools.js) and [New file](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/blob/cbia-rels-compat/src/data/builder-tools/enriched-tools.js)

- Dependency Graph **documentation**

  - We've included documentation in the repository itself [here](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/blob/cbia-rels-compat/readme.cbia.md)




## Milestone #3 - “Ms3-Matrix”

**Acceptance criteria:** *"Our Fork of the Dev portal will render a Trait matrix/table. This will enable projects to clearly see updates for the components they depend on, and identify which other components depend on themselves."*

### Evidence of milestone completion

- Trait Matrix [running website here](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/). Each feature below links to the exact view shown. We highlight some features:

  - **From any tool's page:** a new branch icon, next to *Share*, on every tool page of the portal (here [Cardano Serialization Library](https://45b.io/cbia-infra-tools-ms3/tools/cardano-serialization-library/)).

![Ms3-ScreenShot01.png](/readme_static/Ms3-ScreenShot01.png)

  - It opens the view focused on that tool: Cardano Serialization Library and the 9 tools that depend on it, 6 of them directly ([view](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?matrix=1&tool=Cardano+Serialization+Library&branch=1)).

![Ms3-ScreenShot02.png](/readme_static/Ms3-ScreenShot02.png)

  - `Trait matrix ▸` opens under the category labels: the dependency tree keeps the upper part of the screen and the matrix takes the lower part, each scrolling on its own ([view](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?matrix=1)).

![Ms3-ScreenShot03.png](/readme_static/Ms3-ScreenShot03.png)

  - **Updates for the components a project depends on:** the *Depends on* column lists each dependency with its latest version, in green when released in the last 90 days. Lucid Evolution depends on 6 listed tools: 3 released recently, while bech32 and cardano-multiplatform-lib haven't released since 2024 and 2025 ([view](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?matrix=1&tool=Lucid+Evolution)).

![Ms3-ScreenShot04.png](/readme_static/Ms3-ScreenShot04.png)

  - **All the way down:** in `Dependencies` mode, the branch icon shows everything a tool relies on, at every depth. With `Soft refs` off, Maestro relies on 9 tools across 3 levels (Maestro → Koios → cardano-db-sync → cardano-api) ([view](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?matrix=1&tool=Maestro&branch=1), then `Dependencies` and untick `Soft refs`).

![Ms3-ScreenShot05.png](/readme_static/Ms3-ScreenShot05.png)

  - **Which other components depend on a project:** the *Depended on by* column counts them (hover for names). In `Dependents` mode, the branch icon shows everything that depends on a tool: 37 tools depend on cardano-node, 18 of them directly ([view](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?matrix=1&tool=cardano-node&branch=1)).

![Ms3-ScreenShot06.png](/readme_static/Ms3-ScreenShot06.png)

  - **Traits**, as defined in Milestone #1, plus the catalog's own: language and interface (from the portal catalog), license (from GitHub), and Cardano capabilities grouped from the CIPs a release names (wallet connection, token metadata, governance, blueprints, message signing). Hover a trait for its source; click it to filter, and traits of different kinds combine: [TypeScript tools with wallet connection](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?lang=typescript&cap=wallet) (8 tools), [governance](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?cap=governance) (5), [token metadata](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?cap=tokens) (6).

![Ms3-ScreenShot07.png](/readme_static/Ms3-ScreenShot07.png)

  - `Trait kinds` picks which kinds are shown. Licenses are stricter than the portal's "Open Source" badge, which only needs a repository link: [3 tools have a license GitHub can't identify](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?license=unknown&kinds=lang,license,cap) and [8 have none detected](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?license=none&kinds=lang,license,cap).

![Ms3-ScreenShot08.png](/readme_static/Ms3-ScreenShot08.png)

  - **Health:** active, stale (no commits for a year), pre-release (no stable release among the last 10), archived. Sorting the column brings up, for example, Lucid and Cardano Node API (archived) and Carp and Scrolls (stale) ([view](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?matrix=1), sort by *Health*).

  - **Two readiness sources** over the same dependency graph: detected from each tool's repository (Conway, the current era), or [Intersect's Dijkstra hard fork readiness tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?usp=sharing) (protocol version 12), per network. The tracker lists a "Compatibility matrix" as a critical-path item; this view adds what a flat list can't show: a tool's own status next to its dependencies' (`blocked by …` when one is behind, and how many have no information yet). Here Koios, on the tracker's critical path, with its 3 dependencies ([view](https://45b.io/cbia-infra-tools-ms3/tools-rels-compat/?matrix=1&tool=Koios&source=intersect)).

![Ms3-ScreenShot09.png](/readme_static/Ms3-ScreenShot09.png)

  - Columns sort on click, a search box filters by name, the category labels filter the matrix too, and clicking a dependency in the matrix brings it into view in the tree. Every view has its own shareable URL, as the links above show.

  - Counts above include soft references (a tool's README naming another), which `Soft refs` adds to the dependencies found in manifests and is on by default. Unticking it leaves hard dependencies only: cardano-node then has 12 direct dependents instead of 18.

- Data operations:

  - Data script: fetching and enriching from GitHub, for all 103 tools now on the upstream portal.

![Ms3-ScreenShot91.png](/readme_static/Ms3-ScreenShot91.png)

  - Data script: final output, applying the human-reviewed overrides and counting tools.

![Ms3-ScreenShot92.png](/readme_static/Ms3-ScreenShot92.png)

  - Readiness sync: mapping Intersect's tracker onto the portal's tools.

![Ms3-ScreenShot93.png](/readme_static/Ms3-ScreenShot93.png)

- Trait Matrix **source code**, on [our fork of the Dev portal](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/tree/cbia-rels-compat-Ms3), rebuilt on the current upstream portal:

  - [Tree and trait matrix component](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/tree/cbia-rels-compat-Ms3/src/components/BuilderToolsTree)
  - [GitHub enrichment script](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/blob/cbia-rels-compat-Ms3/scripts/analyze-builder-tools.mjs) and [Intersect tracker sync script](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/blob/cbia-rels-compat-Ms3/scripts/sync-intersect-readiness.mjs)
  - Data: [enriched tools](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/blob/cbia-rels-compat-Ms3/src/data/builder-tools/enriched-tools.json), [curated overrides](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/blob/cbia-rels-compat-Ms3/src/data/builder-tools/enriched-overrides.js) and [tracker readiness](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/blob/cbia-rels-compat-Ms3/src/data/builder-tools/intersect-readiness.js)

- Trait Matrix **documentation**, in the repository itself [here](https://github.com/CardanoBlockchainInfraAlliance/developer-portal-cbia/blob/cbia-rels-compat-Ms3/README.CBIA.md)

## Final Milestone  - “Ms4-Report”

**Acceptance criteria:** *"Project Closeout Report, including a close-out video, is according to standard and includes learnings to share with the community."*

### Evidence of milestone completion

- Project Completion Report https://drive.google.com/file/d/1WlNKoWBYzKNa88eIeDpq2Bhb9R4NBr8j/view?usp=sharing
- Project Completion Video (Project links in description [including PCR with learnings]) https://youtu.be/1_wWhE-WEEY
- Project Completion Video Tweet https://x.com/cbia_org/status/2107912809371574780
- Our Website https://cbia.io/#projects

