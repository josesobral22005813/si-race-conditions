SI: Race Conditions
=================================
NOTE: This repository was created as part of the 'Segurança Informática' course at Universidade Lusófona, for the presentation of an OWASP Top 10-style project on Race Conditions.

| Threat agents/Attack vectors | Security Weakness | Impacts |
| - | - | - |
| API Specific : Exploitability **2** | Prevalence **2** : Detectability **1** | Technical **3** : Business Specific |
| Critical sections of code usually have a very narrow timing window to perform an exploit using a race condition, so an attacker would have to be very persistent with his calls to the API, which could induce a timeout from an API with rate limiting. If the timing window is higher for a critical section, the exploit is easier to perform and requires little technical background from an attacker | APIs allow multiple connections to be established to one or multiple endpoints, opening multiple threads on the server to process the request of a user, so often developers have a lack of understanding or forget about the 'hidden' factor of multithreading in API development. Methods of black box are an hard way of detecting this exploit, and due to most APIs not being open source and only making its endpoints public, white box is hard to be done in this cases | Race conditions in an API commonly leads to unexpected modifications of information like variables or values in a database, which can lead to modification of sensitive or important information |

## Is the API Vulnerable?

The API relies on shared resources that can be accessed by multiple connections to it,
such as databases or variables, and the resources are accessed and modified by those
threads, with a lack of synchronization mechanisms, such as semaphores. If the code is
open source an attacker could detect a logical error in one or multiple functions and
exploit the API.

## Example Attack Scenarios

### Scenario #1

A popular Coffeehouse company implemented a gift card system thru a mobile app, allowing users to add balance to that gift card and transfer balance from one gift card to another. The API responsible for the mobile app logic had a resource for the "account balance", which is a shared resource by the transfer balance call. The API function would check the balance to see if it was equals or greater to the balance to transfer, after that check, the money is subtracted from the card balance and added to the other card.
After the attacker extracted the API call thru a proxy, he created a script to send the same API call of transfering 100$ from his gift card to another gift card owned by him, 2 times in a row. The first thread created by the first API call checked the balance from the account and before it subtracted from the gift card, the second thread created by the second API call checked again the balance from the account, so the check was passed by both threads. If the card has a balance of less than 200$, after transfering the money to another card, the first card was left with a negative balance, and the other card with 200$. 

## How To Prevent

* Analyze your code thru 'White Boxing', essencially reviewing the source code assessing all the code and identifying logic that is assuming synchronous actions.
* Implement locking mechanisms such as semaphores to protect critical sections.
* Perform stress-tests to your API before sending changes to production.
* Be always aware that connections can be made at the same time, so design and implement your API as such.

## References

### External

* [CWE-362: Concurrent Execution using Shared Resource with Improper Synchronization ('Race Condition')][1]
* [Hacking Starbucks for unlimited coffee][2]

[1]: https://cwe.mitre.org/data/definitions/362.html
[2]: https://sakurity.com/blog/2015/05/21/starbucks.html
