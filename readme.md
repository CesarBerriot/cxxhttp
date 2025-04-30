# cxxhttp
Automates the integration of curlpp, curl, mbedtls, http-status-codes-cpp and the latest curl CA certificate bundle, all built from source.

### Usage
1. Fetch the latest release of this repository.
2. Include `cxxhttp.cmake` from its root directory.
3. Set the following variables to `OFF` according to your needs (all `ON` by default) : `CXXHTTP_INTEGRATE_CURLPP`, `CXXHTTP_INTEGRATE_HTTP_STATUS_CODE`, `CXXHTTP_INTEGRATE_CA_CERTIFICATE_BUNDLE`.
4. Call `cxxhttp_setup_target(<your target>)`.

### Options Reference
| Option                                    | Description                                                                              |
|-------------------------------------------|------------------------------------------------------------------------------------------|
| `CXXHTTP_INTEGRATE_CURLPP`                | Integrates curlpp, curl and mbedtls.                                                     |
| `CXXHTTP_INTEGRATE_HTTP_STATUS_CODE`      | Integrates [http-status-codes-cpp](https://github.com/j-ulrich/http-status-codes-cpp).   |
| `CXXHTTP_INTEGRATE_CA_CERTIFICATE_BUNDLE` | Integrates the latest [curl CA certificate bundle](https://curl.se/docs/caextract.html). |

### Using the bundled CA certificates
Bundled CA certificates are made available through a globally accessible `curl_blob` called `ca_certificates` and can be used in the following manner :
```cpp
using namespace curlpp;
Easy request;
request.setOpt<OptionTrait<curl_blob*, CURLOPT_CAINFO_BLOB>>(&ca_certificates);
request.setOpt<options::Url>("https://www.example.com");
request.perform();
```