# Versions

Note versions of the tooling employed. This is not exhaustive, but helps in troubleshooting if results are unpredictable.

The DDCC IG is tested against the latest release versions of the primary components in the workflow. This holds the other components relatively constant and focuses on differences of the main branch of DDCC, rather than testing against different versions of tooling. Components should be tested in their own repositories. The objective is to test the DDCC IG itself and not against not a matrix of versions of components.

| **DDCC Components** | Version | Notes |
| --- | --- | --- |
| DDCC IG | **head of main branch** | All runs use the latest main branch |
| DDCC Transactions Mediator | **head of main branch** | All runs use the latest main branch |
| HAPI FHIR Server | **5.4.1** |  |


| **Requirements** | Version | Notes |
| --- | --- | --- |
| Ubuntu (ubuntu-latest) | **20.04** | GitHub Actions (nektos/act image is different)  |
| FHIR | **4.0.1** | |
| Node | **16.x** LTS | |
| Jekyll | **4.2.0** | |
| Sushi | **2.1.1** | Will be updated due to frequent bug fixes |
| Java | **11.x** | Eclipse Temurin (formerly AdoptOpenJDK) |
| Publisher | **1.1.77** | Will be updated due to frequent bug fixes |


