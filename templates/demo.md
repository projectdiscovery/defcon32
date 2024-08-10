## Profile

cat all-httpx.txt | nuclei -profile cves

## AWS bucket takeover

cat targets.txt | katana -srd “bugbounty-data/workshop”

echo "bugbounty-data/redacted/" | nuclei -t aws-bucket-takeover-example.yaml -code -debug

## Burp Requests Scanning

nuclei -dast -l test -im burp

nuclei -id cookie-injection -td

## Asset Upload
cat all-bugbounty-targets.txt | httpx -dashboard

https://cloud.projectdiscovery.io/assets/cqlnmsv3amss739vudig?type=all
