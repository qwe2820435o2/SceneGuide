# Code review template

## 1. Improve the basic information of the review meeting

### 1.1 Description of Requirement

example: 

The current statistical count involves multiple content modules, including: col, artist, music, buzz, video, podcast, etc., and multiple projects are involved in the middle

The stacking method of each project is different, including direct stacking of the database, and regular refresh of the cache to the database stacking. There is no unified stacking specification.

This not only has an impact on the technical statistical performance, but also is not conducive to the formation of a unified ability, so...

### 1.2 Detail information

| Conference theme   |      (Example: Statistical counting capability independent service)              |
| ---------- | :--------------------------------------------- |
| Sponsor     |                  (Example: kris)                  |
| Place       | 150 Tanglin Road，Singapore |
| Time       |          2022-05-27                            |
| Meeting host |               (Example: kris)                   |
| Conference judges   |          (Example: kris，tom)              |


## 2. Review related materials

| Review information | Details                                                         |
| -------- | :----------------------------------------------------------- |
| Involved projects |  platform-counting-service，platform-counting-bg   |
| Involving branches | fix-stream-calculate |
| Development program |                         |
| flow chart  |  |
| data model |                              |

## 3. Review rules

## 3.1 classification

| problem level | detail                                                         |
| ---------- | :----------------------------------------------------------- |
| S          |             **Required**, which affects the function                            |
| A          |                    **Required**, which affects performance                    |
| B          | Optimization : comment/log/code specification (host: for new/independent services, use the Ali plug-in to scan it again), it is strictly forbidden to encapsulate objects with Map |
| C          |          Suggestion/optimization , class code is too long, too many judgments, hard-coded          |

## 3.2 question type

## 4. Review process

## 5. Review report