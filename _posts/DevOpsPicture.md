                         DEVELOPER
                             │
                             │ Code
                             ↓
                            Git
                             │
                             ↓
                          Jenkins
                             │
                  ┌──────────┼──────────┐
                  ↓          ↓          ↓
                Build       Test    Docker Build
                                        │
                                        ↓
                                  Docker Image
                                        │
                                        ↓
                                Docker Registry
                                        │
                                        ↓
                              Kubernetes Cluster
                                        │
                     ┌──────────────────┼──────────────────┐
                     ↓                  ↓                  ↓
                 Worker Node        Worker Node        Worker Node
                     │                  │                  │
                    Pod                Pod                Pod
                     │                  │                  │
                Container          Container          Container
                     │                  │                  │
                Spring Boot       Spring Boot       Spring Boot
                     │                  │                  │
                     └──────────────────┼──────────────────┘
                                        ↓
                                      Users