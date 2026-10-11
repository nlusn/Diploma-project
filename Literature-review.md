# 3. Literature Review

## 3.1 How the sources were found

I ran five searches in Scopus. The exact queries, filters and counts are in Appendix A.
The first three cover 2022 onwards, the last two 2023 onwards. I also found one review,
El-Rajab 2025, through a web search and read it on the publisher's page.

| Search | Topic | Records | Result |
|--------|-------|---------|--------|
| 1 | few-shot and fine-grained image classification, transfer learning | 8,190 | one survey on data scarcity |
| 2 | pose estimation for exercise feedback | 769 | six papers |
| 3 | gym or fitness machines with image classification, detection or YOLO | 42 | two papers, none of which recognises a machine from a photo |
| 4 | resistance training, injuries, beginners, technique | 130 | two papers (lots of gymnastics hits, so I went through them by hand) |
| 5 | fitness apps and usability | 490 | one paper (most were clinical studies) |

## 3.2 Analysis table

| ID | Source | What they did | Result | Limitation they report | Why it matters here |
|----|--------|---------------|--------|------------------------|---------------------|
| S1 | Hsieh et al., 2026 (IJETI) | YOLOv8 segmentation and edge detection to measure back angle with a phone camera | 6.49% mean relative error on six gym videos | Small dataset, camera placement matters, body orientation had to be given as input. The authors say a lightweight mobile tool for self-guided gym training is still missing. | Closest work to this project: gym, phone camera, YOLO |
| S2 | Rao et al., 2025 (IEEE Access) | Squat analysis from stereo video with MediaPipe and a Bi-CGRU model | 96.1% classification accuracy | Single-camera setups are a problem; depth information is left for future work | Shows people want guidance without paying for a trainer |
| S3 | Garg et al., 2023 (CHASE) | Exercise feedback for four physical-therapy exercises from one smartphone camera | Correctness classification and guidance were feasible | The authors note there is little work using only one RGB camera | Supports a phone-only design |
| S4 | El-Rajab et al., 2025 (Front. Sports Act. Living) | Systematic review of camera-based mobile apps for movement screening | Apps are cheap and accessible, but accuracy and feedback are still weak | More real-time feedback and a wider range of movements are needed | Shows where this project sits among camera-based apps |
| S5 | Frangoudes et al., 2022 (IEEE Access) | Review of 88 papers (2017 to 2021) on machine learning for exercise assessment | Good systems should be personal, explainable and real-time | Small datasets and a lack of large open ones | Why I plan to add my own gym photos |
| S6 | Alves et al., 2025 (ACM) | RepVal, a skeleton-based repetition checker, with a new dataset (64 videos, 8 people, 3 exercises) | Ran on several edge devices with quick feedback | Few fitness datasets exist | On-device inference looks realistic, and these datasets are small |
| S7 | Chang et al., 2024 (IEEE Access) | OpenPose angles and a 1D-CNN to detect wrong rowing technique | 96.65% accuracy on 1,155 sequences | Dataset needs to grow; it covers one machine only | Machine-specific, but not a general recogniser |
| S8 | Sideridou et al., 2024 (Sensors) | BlazePose and classifiers to recognise exercises, 57 volunteers, 5 exercises | 94.76% to 100% accuracy | Some limits of the BlazePose implementation | A mobile tool for beginners without a trainer |
| S9 | Petushek et al., 2026 (JSCR) | Technique quiz for 310 exercise professionals | Average score 50%; 97% wanted to learn more | Research on this skill is lacking; participants came from snowball recruiting | Even professionals score low, so clear guidance has value |
| S10 | Noteboom et al., 2024 (Front. Physiol.) | Musculoskeletal modelling of bench press variations | Narrower grips and scapula retraction lowered modelled shoulder loads | Not a study of real injuries; little evidence on technique and injury | A reason to keep the safety advice general |
| S11 | Sapkota et al., 2025 (Artif. Intell. Rev.) | Review of YOLO from v1 to v12 | Small variants exist for edge devices, trading some accuracy for speed | Weaker performance on low-power hardware | Basis for choosing YOLO |
| S12 | Howard et al., 2019 (MobileNetV3) | Network designed for phone CPUs | Better accuracy for the same latency | Not applicable | The lightweight alternative |
| S13 | Radford et al., 2021 (CLIP) | Image classification from text descriptions, no labelled examples | Works zero-shot on new tasks | Not applicable | The option for machines missing from the training set |
| S14 | Alzubaidi et al., 2023 (J. Big Data) | Survey of ways to train deep models with little data | Transfer learning and augmentation are the usual fixes | Not applicable | Fits the small-dataset risk in this project |
| S15 | Gao et al., 2025 (JMIR Serious Games) | Two-month study of an AI fitness app with 456 students, usability measured with SUS | SUS score of 65.2 | Short follow-up, engagement dropped after about five weeks, no health outcomes | A model for how to evaluate my app |

## 3.3 What the literature shows

Most work on exercise recognition looks at the person, not the equipment. Pose-based
systems can recognise or judge squats, rowing, physical-therapy moves and functional
fitness repetitions, and three of them report accuracy above 94% on their own data
(Rao et al. 2025; Chang et al. 2024; Sideridou et al. 2024). Hsieh et al. (2026) used
YOLOv8 to measure back angle in a gym with an ordinary phone, with a mean error of
6.49% on six videos. Two reviews cover the field (El-Rajab et al. 2025; Frangoudes et
al. 2022). El-Rajab points to accuracy, real-time feedback and a narrow range of
movements, and Frangoudes to small datasets.

The same problems keep coming back. Datasets are small or not public (Hsieh et al.
2026; Frangoudes et al. 2022; Alves et al. 2025). Rao's system needs a stereo camera,
and Garg et al. (2023) say earlier work leans on costly special sensors. Exercise
coverage is narrow too: Chang's rowing study covers a single machine, and El-Rajab asks
for more types of movement. Garg also notes that hardly anything uses only a single
phone camera.

Technique knowledge is uneven, even among professionals. In the quiz by Petushek et al.
(2026) the average score was 50%, and 97% of the 310 professionals wanted to learn
more. The bench press model by Noteboom et al. (2024) links grip width and scapula
position to shoulder load, but it says nothing about real injuries. For a beginner app
that means general safety advice and nothing that sounds like medical advice.

For the recognition model I see three options: YOLO, which has many versions and small
variants for phones (Sapkota et al. 2025); MobileNetV3, built for mobile CPUs (Howard
et al. 2019); and CLIP, which can classify from text labels alone (Radford et al.
2021). Whichever I pick, the small dataset is the biggest risk. The survey by Alzubaidi
et al. (2023) lists the usual ways to deal with it, such as transfer learning and
augmentation.

Gao et al. (2025) tested an AI fitness app with the System Usability Scale and followed
usage over time. I plan to measure usability and retention the same way.

## 3.4 Research gap

Among the sources I reviewed, camera-based gym systems look at how the person moves
(Hsieh et al. 2026; Rao et al. 2025; Garg et al. 2023; Chang et al. 2024; Sideridou et
al. 2024). The only machine-specific study covers a single rowing machine, and it checks
technique, not which machine is which (Chang et al. 2024). I did not find a study that
works out which gym machine is in a photo and then gives instructions for it. That
comes from my own search (Appendix A, search 3), so I am not saying nothing like it
exists anywhere.

Some related gaps are stated by the authors themselves: approaches that use only a
single phone camera are rare (Garg et al. 2023), datasets are small (Hsieh et al. 2026;
Frangoudes et al. 2022; Alves et al. 2025), and reliable knowledge about technique is
limited (Petushek et al. 2026; Noteboom et al. 2024).

This project tries to cover the first gap in three steps. It recognises the machine
from a photo, returns guidance from a prepared knowledge base, and answers "unknown
machine" when the model isn't confident enough. I will test it on a separate set of
photos taken in real gyms.

## 3.5 Limits of this review

- It is not a systematic review. I used one database, five queries and one web search.
- Several sources are conference papers or come from smaller journals, and each
  accuracy figure comes from that study's own data, so the numbers can't be compared
  with each other.

## 3.6 References

Check every DOI on the publisher page before committing.

1. Hsieh, P.-H., Choi, H. S., Hsu, H.-Y. (2026). Int. J. Eng. Technol. Innov., 16(2), 163-178. DOI 10.46604/ijeti.2026.15942
2. Rao, P., Asha, C. S., Rao, P. R. (2025). IEEE Access. DOI 10.1109/ACCESS.2025.3545207
3. Garg, B., Postlmayr, A., Cosman, P., Dey, S. (2023). IEEE/ACM CHASE. DOI 10.1145/3580252.3586984
4. El-Rajab, I. et al. (2025). Front. Sports Act. Living. DOI 10.3389/fspor.2025.1531050
5. Frangoudes, F. et al. (2022). IEEE Access. DOI 10.1109/ACCESS.2022.3198935
6. Alves, L., Li, F., Xu, L. (2025). RepVal. ACM. DOI 10.1145/3769102.3774242
7. Chang, R., Yang, Z., Ning, J. (2024). IEEE Access. DOI 10.1109/ACCESS.2024.3445875
8. Sideridou, M. et al. (2024). Sensors, 24(7), 2037. DOI 10.3390/s24072037
9. Petushek, E. et al. (2026). J. Strength Cond. Res. DOI 10.1519/JSC.0000000000005249
10. Noteboom, L. et al. (2024). Front. Physiol. DOI 10.3389/fphys.2024.1393235
11. Sapkota, R. et al. (2025). Artif. Intell. Rev., 58, 274. DOI 10.1007/s10462-025-11253-3
12. Howard, A. et al. (2019). Searching for MobileNetV3. ICCV. Cite the CVF open-access page.
13. Radford, A. et al. (2021). Learning transferable visual models from natural language supervision. PMLR 139. No DOI.
14. Alzubaidi, L. et al. (2023). J. Big Data, 10, 46. DOI 10.1186/s40537-023-00727-2
15. Gao, Y. et al. (2025). JMIR Serious Games. DOI 10.2196/65498

---

## Appendix A. Search log

Searches were run in Scopus. One review (El-Rajab 2025) was found by a web search outside Scopus.

| # | Query (exact string) | Filters | Results | Kept |
|---|----------------------|---------|---------|------|
| 1 | TITLE-ABS-KEY(("fine-grained" OR "few-shot" OR "long-tail") AND ("image classification" OR "image recognition") AND ("transfer learning" OR "pretrained")) | PUBYEAR > 2021 | 8,190 | 1 |
| 2 | TITLE-ABS-KEY(("pose estimation" OR "human pose") AND (exercise OR fitness OR workout OR "resistance training") AND (feedback OR correction OR "form")) | PUBYEAR > 2021 | 769 | 6 |
| 3 | TITLE-ABS-KEY(("gym equipment" OR "fitness machine" OR "exercise machine" OR "strength training machine" OR "weight machine") AND ("image classification" OR "object detection" OR "image recognition" OR YOLO OR CNN)) | PUBYEAR > 2021 | 42 | 2 |
| 4 | TITLE-ABS-KEY(("resistance training" OR gym) AND injur* AND (beginner OR novice) AND (technique OR "exercise form" OR instruction)) | PUBYEAR > 2022 | 130 | 2 |
| 5 | TITLE-ABS-KEY(("fitness app" OR "exercise app") AND (usability OR "user experience" OR "System Usability Scale")) | PUBYEAR > 2022 | 490 | 1 |

### Where each source came from

| ID | Source | Origin |
|----|--------|--------|
| S1 | Hsieh 2026 | Search 3 |
| S2 | Rao 2025 | Search 2 |
| S3 | Garg 2023 | Search 2 |
| S4 | El-Rajab 2025 | Web search for reviews on camera-based exercise apps (publisher page read; not in a Scopus export) |
| S5 | Frangoudes 2022 | Search 2 |
| S6 | Alves 2025 | Search 2 |
| S7 | Chang 2024 | Search 2 |
| S8 | Sideridou 2024 | Search 2 |
| S9 | Petushek 2026 | Search 4 |
| S10 | Noteboom 2024 | Search 4 |
| S11 | Sapkota 2025 | Search 3 |
| S12 | Howard 2019 | Foundational (cited from CVF page) |
| S13 | Radford 2021 | Foundational (PMLR 139) |
| S14 | Alzubaidi 2023 | Search 1 |
| S15 | Gao 2025 | Search 5 |