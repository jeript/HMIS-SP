# Hash Client IDs

Since HMIS Client IDs are technically PII when generating reports with client IDs it is a good idea to create a hash of those IDs. This can only be returned back to the HMIS ID if the prime number used to generate the hash is known.
2654435761 is the prime number being used here but other prime numbers can be used as well to make your hash unique.

```
=Mod([Client Uid]*2654435761;4294967296)
```
