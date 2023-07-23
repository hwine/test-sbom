# test-sbom

A playground to see understand some of the SBOM options, and usage thereof.

Tools are still evolving in the space, so the quirks of each needs to be understood.

## To Do
_[Roughly - details will be in issues.]_

- understand depth of dependency tree captured by each SBOM generator.
- understand how vulnerability data can be integrated (i.e. are there "vex like" features)

## Preliminary Notes

### GitHub SBOMS

The workflow [workflow](.github/workflows/generate-and-commit-github-sboms.yaml)
uses existing GitHub Actions to capture the current GitHub generated SBOM for
various repositories. The output is then pretty printed into a file and
committed to the repository as `githb/{organization_name}/{repository_name}.json`.

Known limitations:
- SBOM is tracked by name, which can by changed by admins
- SBOM is not identified as to which revision of the repository it reflects.
- Every SBOM document has both a random string, and the current date/time in it.
  Thus "git changes" are present even if no structural changes are identified.
  - the random strings could be removed during pretty printing

### Anchore SBOMS and tooling

For reasons I have yet to determine, the Anchore vulnerability analysis tool
`grype` does not properly read a GitHub generated SBOM. The tool does work well
with Anchore `syft` produced SBOMS, which can also be generated via a GitHub
workflow.
