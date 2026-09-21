# Task-by-Task Progress Log

## Task 1: Setup and Understand the Environment
Changes made:
- Reviewed the project structure and identified the main workflow components.
- Updated the project documentation in [README.md](README.md) to explain the monitored service, the operational problem, and the purpose of AIOps in the assessment.

Git commands to use after completing this task:
    git status
    git add README.md
    git commit -m "Task 1: document AIOps setup and scenario"
    git push origin main

## Task 2: Prepare and Inspect Operational Data
Changes made:
- Inspected [data/service_data.json](data/service_data.json) to identify metrics, logs, timestamps, and normal vs abnormal observations.
- Recorded the findings in [README.md](README.md).

Git commands to use after completing this task:
    git status
    git add README.md data/service_data.json
    git commit -m "Task 2: analyze operational metrics and logs"
    git push origin main

## Task 3: Identify Anomalies
Changes made:
- Fixed the anomaly logic in [src/anomaly_detector.py](src/anomaly_detector.py) so it flags error-level logs instead of warning-level noise.
- Kept the existing architecture and logic flow while correcting the root cause.

Git commands to use after completing this task:
    git status
    git add src/anomaly_detector.py README.md
    git commit -m "Task 3: fix anomaly detection logic"
    git push origin main

## Task 4: Verify the AIOps Event Flow
Changes made:
- Fixed the event pipeline in [src/aiops_pipeline.py](src/aiops_pipeline.py) so the producer and consumer use the same in-memory topic.
- Validated the producer-to-consumer flow required by the assessment.

Git commands to use after completing this task:
    git status
    git add src/aiops_pipeline.py README.md
    git commit -m "Task 4: correct event propagation in pipeline"
    git push origin main

## Task 5: Troubleshoot and Demonstrate Workflow
Planned changes:
- Confirm the end-to-end AIOps pipeline runs successfully.
- Verify the final anomaly event reaches the downstream output step.
- Document the workflow result and any remaining improvements.

Git commands to use after completing this task:
    git status
    git add src/aiops_pipeline.py README.md
    git commit -m "Task 5: verify end-to-end workflow"
    git push origin main

## Task 6: Execute the End-to-End Pipeline
Planned changes:
- Run the complete operational data → anomaly detection → event → producer → topic → consumer → AIOps output workflow.
- Capture the observable result for the final documentation.

Git commands to use after completing this task:
    git status
    git add src/aiops_pipeline.py README.md
    git commit -m "Task 6: execute complete AIOps flow"
    git push origin main

## Task 7: Update the README
Planned changes:
- Ensure the README includes scenario, data analysis, anomaly findings, event flow description, execution result, corrections, limitation, and reproduction steps.

Git commands to use after completing this task:
    git status
    git add README.md
    git commit -m "Task 7: document findings and reproduction steps"
    git push origin main

## Task 8: Validate the Project
Planned changes:
- Run the repository validation tests and resolve any remaining issues.

Git commands to use after completing this task:
    git status
    git add .
    git commit -m "Task 8: validate AIOps workflow and tests"
    git push origin main

## Task 9: Final Commit and Push
Planned actions:
- Review the final diff.
- Make sure only assessment-related updates remain.
- Commit and push the final repository state.

Git commands to use after completing this task:
    git status
    git add .
    git commit -m "Task 9: finalize AIOps assessment"
    git push origin main
