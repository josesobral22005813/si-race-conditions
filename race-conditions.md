# si-race-conditions
SI: Race Conditions
=================================
Este repositório foi criado no âmbito da Unidade Curricular de Segurança Informática da Universidade Lusófuna, para a exposição de um trabalho estilo OWASP Top 10 sobre Race Conditions. 



| Threat agents/Attack vectors | Security Weakness | Impacts |
| - | - | - |
| API Specific : Exploitability **3** | Prevalence **2** : Detectability **2** | Technical **2** : Business Specific |
| Exploitation of Excessive Data Exposure is simple, and is usually performed by sniffing the traffic to analyze the API responses, looking for sensitive data exposure that should not be returned to the user. | APIs rely on clients to perform the data filtering. Since APIs are used as data sources, sometimes developers try to implement them in a generic way without thinking about the sensitivity of the exposed data. Automatic tools usually can’t detect this type of vulnerability because it’s hard to differentiate between legitimate data returned from the API, and sensitive data that should not be returned without a deep understanding of the application. | Excessive Data Exposure commonly leads to exposure of sensitive data. |

## Is the API Vulnerable?


## Example Attack Scenarios

### Scenario #1


### Scenario #2


## How To Prevent



## References

### External

* [CWE-362: Concurrent Execution using Shared Resource with Improper Synchronization ('Race Condition')][1]

[1]: [https://cwe.mitre.org/data/definitions/213.html](https://cwe.mitre.org/data/definitions/362.html)
