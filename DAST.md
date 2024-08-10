# DAST (Dynamic Application Security Testing) or Fuzzing

To follow along, you need to install a local fuzz playground on which you want to run templates

```console
go install -v github.com/projectdiscovery/nuclei/v3/cmd/tools/fuzzplayground@latest
```

### Run Fuzz Playground in Another Tab of Terminal

```
fuzzplayground
```

### List All Possible Parameters and Execute Template

```console
nuclei -u localhost:8082 -dast -l dast/testData/proxify.yaml -im yaml -t dast/fuzz-generic-sqli.yaml -dfp    
```

### Checkout Docs for more information

- [Nuclei](https://docs.projectdiscovery.io/tools/nuclei/overview)
- [Nuclei-Templates](https://docs.projectdiscovery.io/templates/introduction)
- [DAST-Template](https://docs.projectdiscovery.io/templates/protocols/http/fuzzing-overview)
