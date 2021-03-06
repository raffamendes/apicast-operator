# APIcast Custom Resource reference

**json/yaml field**| **Type** | **Required** | **Default value** | **Description** |
| --- | --- | --- | --- | --- |
| `spec` | [APIcastSpec](#APIcastSpec) | Yes | See [APIcastSpec](#APIcastSpec) | The specfication for Apicast custom resource |
| `status` | [APIcastStatus](#APIcastStatus) | No | See [APIcastStatus](#APIcastStatus) | The status for the custom resource  |

#### APIcastSpec

**json/yaml field**| **Type** | **Required** | **Default value** | **Description** |
| --- | --- | --- | --- | --- |
| `replicas` | integer | No | 1 | Number of replica pods |
| `adminPortalCredentialsRef` | LocalObjectReference | No | N/A | Secret with the portal endpoint URL information. See [AdminPortalSecret](#AdminPortalSecret) for required format |
| `embeddedConfigurationSecretRef` | LocalObjectReference | No | N/A | Secret containing the gateway configuration. See [EmbeddedConfSecret](#EmbeddedConfSecret) for required format |
| `serviceAccount` | string | No | `default` service account | Service account associated to the gateway |
| `image` | string | No | Official apicast image | Apicast gateway container image. Only for devtesting purposes |
| `exposedHost` | [APIcastExposedHost](#APIcastExposedHost) | No | No external access | Domain name used for external access |
| `deploymentEnvironment` | string | No | N/A | Environment for which the configuration (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#threescale_deployment_env)) |
| `dnsResolverAddress` | string | No | N/A | DNS resolver (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#resolver)) |
| `enabledServices` | []string | No | N/A | List of service IDs used to filter the services configured (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#apicast_services_list)) |
| `configurationLoadMode` | string | No | N/A | Defines how to load the configuration (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#apicast_configuration_loader)) |
| `logLevel` | string | No | N/A | Log level for the OpenResty logs  (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#apicast_log_level)) |
| `pathRoutingEnabled` | bool | No | N/A | When this parameter is set to true, the gateway will use path-based routing in addition to the default host-based routing (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#apicast_path_routing)) |
| `responseCodesIncluded` | bool | No | N/A | When set to true, APIcast will log the response code of the response returned by the API backend in 3scale (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#apicast_response_codes)) |
| `cacheConfigurationSeconds` | integer | No | N/A | Specifies the period (in seconds) that the configuration will be stored in the cache (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#apicast_configuration_cache)) |
| `managementAPIScope` | string | No | N/A | Apicast management API configuration control (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#apicast_management_api)) |
| `openSSLPeerVerificationEnabled` | bool | No | N/A | Controls the OpenSSL Peer Verification (see [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#openssl_verify)) |

#### APIcastStatus

Used by the Operator/Kubernetes to control the state of the Apicast custom resource. It should never be modified by the user.

| **json/yaml field** | **Type** | **Description** |
| --- | --- | --- |
| `image` | string | The image being used in the APIcast deployment |

#### APIcastExposedHost

| **json/yaml field** | **Type** | **Required** | **Default value** | **Description** |
| --- | --- | --- | --- | --- |
| `host` | string | Yes | N/A | Domain name being routed to the gateway |
| `tls` | []extensions.IngressTLS | No | N/A | Array of ingress TLS objects (see [doc](https://kubernetes.io/docs/concepts/services-networking/ingress/#tls)) |

#### AdminPortalSecret

| **Field** | **Description** |
| --- | --- |
| AdminPortalURL | URI that includes your password and 3scale [Porta](https://github.com/3scale/porta/) portal endpoint. See [format](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#threescale_portal_endpoint) |

#### EmbeddedConfSecret

| **Field** | **Description** |
| --- | --- |
| `config.json` | JSON file with the configuration for the gateway. See [docs](https://github.com/3scale/APIcast/blob/master/doc/parameters.md#threescale_config_file) |