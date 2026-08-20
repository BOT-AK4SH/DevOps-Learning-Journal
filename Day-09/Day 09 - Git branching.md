# Day 09 - Git Branching Strategy

### 1. Git Branching Strategy

A **Git branching strategy** is a structured method for creating, using, merging, and deleting branches during software development.

It defines:

- Where active development takes place.
- How new features are developed without disturbing stable code.
- How a release is prepared and tested.
- How urgent production defects are fixed.
- How completed changes are returned to the main codebase.

A clear branching strategy helps an organization deliver new features and fixes to customers on schedule while protecting the stability of the existing application.

### 2. Why a Branching Strategy Is Required

Software applications continue to change after their initial release. Developers may simultaneously:

- Add new functionality.
- Correct existing defects.
- Prepare the next product release.
- Test a stable version.
- Resolve an urgent production problem.

If every developer makes changes directly to the same branch, incomplete or breaking changes can affect working functionality. Separate branches provide controlled development areas for different types of work.

An effective branching strategy supports:

| Requirement | How branching helps |
| --- | --- |
| **Stable existing functionality** | New work remains isolated until it is tested. |
| **Parallel development** | Different teams can work on separate features at the same time. |
| **Predictable releases** | A fixed set of changes can be stabilized on a release branch. |
| **Frequent delivery** | Features and fixes can move through a repeatable workflow. |
| **Urgent production fixes** | A short-lived hotfix branch can address a critical issue quickly. |
| **Current integrated code** | Approved changes are merged back into the main branch. |

### 3. What Is a Git Branch?

A **branch** is an independent line of development created from an existing point in a repository.

It allows developers to change code without immediately modifying the stable or shared version. Once the work has been completed and tested, the branch can be merged into the appropriate target branch. A temporary branch may then be deleted.

#### Calculator example

Assume that a calculator currently supports:

- Addition
- Subtraction
- Multiplication
- Division

A new version must introduce advanced capabilities such as percentage calculations. Developing this large change directly on the main branch could affect the working calculator.

A safer process is:

1. Create a feature branch from the current main branch.
2. Develop the percentage functionality on that feature branch.
3. Test both the existing and new functionality.
4. Merge the feature branch into the main branch after successful validation.
5. Delete the feature branch when it is no longer required.

This isolates unfinished work while preserving the existing application.

### 4. Core Branch Types

The branching strategy described here uses four primary branch types:

| Branch type | Main purpose | Typical lifetime | Merged into |
| --- | --- | --- | --- |
| **Main, master, or trunk** | Holds the latest integrated code and supports ongoing development | Long-lived | Remains the central branch |
| **Feature branch** | Isolates development of a new or potentially breaking feature | Temporary | Main branch |
| **Release branch** | Stabilizes, tests, builds, and delivers a specific release | Exists for a release or supported version | Product release; relevant corrections return to main |
| **Hotfix or bugfix branch** | Corrects an urgent defect in a released production version | Very short-lived | Relevant release branch and main branch |

> **Important:** Branch names differ between repositories. Some projects use **main**, others use **master** or **trunk** for the primary development branch.

### 5. Main, Master, or Trunk Branch

The **main branch** is the central integration branch in the repository.

Its responsibilities include:

- Holding the latest accepted code changes.
- Receiving completed feature work.
- Remaining current with fixes made elsewhere.
- Serving as the source from which a future release branch is created.
- Supporting continued active development after a release branch has been created.

The main branch must be kept up to date. If a correction is made only on a release or hotfix branch and is not returned to main, the same defect may reappear in a future release.

In the strategy covered here:

- **Active development** continues on main and feature branches.
- **Customer releases** are built from release branches.

### 6. Feature Branch

A **feature branch** is created to develop a new feature separately from the main codebase.

Feature branches are especially useful when:

- The feature is large.
- The work may take several days or months.
- Multiple developers need to collaborate on the same feature.
- The change could break existing functionality.
- The feature requires independent testing before integration.

#### Feature branch lifecycle

1. Create the feature branch from the latest suitable point on main.
2. Develop and commit the new functionality on the feature branch.
3. Test the feature and verify that existing behavior is not broken.
4. Merge the completed feature into main.
5. Delete the feature branch after integration if it is no longer needed.

#### Example feature names

- **feature-percentage**
- **feature-advanced-calculator**
- **feature-bikes**
- **feature-intercity**

Multiple feature branches may exist simultaneously. For example, one team may develop percentage calculations while another team develops exponent calculations. Each feature remains isolated until it is ready to merge.

### 7. Release Branch

A **release branch** is created when a selected set of features and fixes is ready for final validation and delivery.

The release branch establishes a stable point in the codebase. Development can continue on main without introducing additional unplanned changes into the release being tested.

#### Why release from a release branch instead of main?

Main may continue to receive active development. During release testing, the team needs a controlled version whose scope does not keep changing.

Creating a release branch allows the team to:

- Freeze the intended release contents.
- Perform end-to-end testing.
- Perform functional testing.
- Correct release-specific problems.
- Build the application from a stable source.
- Ship the tested version to customers.
- Continue developing future changes on main.

#### Release branch workflow

1. Merge approved feature branches into main.
2. Select a stable point from main.
3. Create a versioned release branch.
4. Stop adding unrelated new features to that release branch.
5. Perform final testing and stabilization.
6. Build and deliver the product from the release branch.
7. Merge relevant release corrections back into main.

Example release branch names include **release-v3** or **release-1.x**.

### 8. Hotfix or Bugfix Branch

A **hotfix branch** is a short-lived branch created to fix a critical problem found in a production release.

Unlike ordinary feature development, a hotfix is urgent. It may exist for only a day or two because the affected customer-facing version must be repaired quickly.

#### Hotfix workflow

1. Identify the production defect and the affected release.
2. Create a hotfix branch for the correction.
3. Implement and test the smallest required fix.
4. Merge the fix into the relevant supported release branch.
5. Build and deliver the corrected release to customers.
6. Merge the same fix into main so future releases also contain it.
7. Apply it to any other supported release branches that require the correction.

#### Critical synchronization rule

A hotfix must not remain only on the release branch.

It should be propagated to:

- The **relevant release branch**, because that is the version delivered to customers.
- The **main branch**, because main must contain the latest accepted fixes.
- Other **supported release branches**, when they contain the same defect.

If the hotfix is omitted from main, a later release created from main may reintroduce the production bug.

### 9. Overall Branching Workflow

flowchart TB
    M["Main / Master / Trunk"]

    M -->|"Create feature"| F["Feature Branch"]
    F -->|"Test and merge"| M2["Main - Feature Merged"]

    M -->|"Cut stable version"| R["Release Branch"]
    R -->|"Build and ship"| C["Customer Release"]
    C -->|"Production issue"| H["Hotfix Branch"]

    H -->|"Patch release"| P["Patched Release"]
    H -->|"Synchronize fix"| M3["Main - Hotfix Merged"]

The normal sequence is:

1. Main contains the latest integrated code.
2. Feature branches are created for independent development.
3. Completed and tested features are merged into main.
4. A release branch is created from a stable point on main.
5. Testing and release stabilization occur on the release branch.
6. The product is built and shipped from the release branch.
7. Urgent production defects are handled through hotfix branches.
8. Hotfixes and relevant release corrections are merged back into main.

### 10. Calculator Workflow Example

Assume a calculator application already supports basic arithmetic.

#### Active development

- Main contains the working calculator.
- Developers continue correcting and improving the existing functionality.

#### New features

- A **feature-percentage** branch is created for percentage calculations.
- A separate **feature-exponent** branch is created for exponent calculations.
- Different developers can work on both features at the same time.

#### Integration

- Each feature is tested independently.
- When a feature is stable, it is merged into main.
- Its temporary branch can then be deleted.

#### Release

- After the planned features and fixes are integrated, a release branch is created from main.
- End-to-end and functional tests run against the release branch.
- The calculator is built and delivered from that stable branch.

#### Production correction

- If customers report a critical calculation error, a hotfix branch is created.
- The tested correction is merged into the supported release branch and main.

### 11. Uber Workflow Example

Assume that an application initially supports only cab bookings.

#### Adding bike bookings

1. Main continues to support and improve cab bookings.
2. A **feature-bikes** branch is created.
3. A separate group of developers builds and tests bike-booking functionality.
4. After validation, the branch is merged into main.
5. The temporary feature branch is deleted.

#### Adding intercity bookings

1. A **feature-intercity** branch is created from the current codebase.
2. Development and testing occur independently.
3. The completed feature is merged into main.

#### Preparing the next version

1. After the planned features are integrated, a **release-v3** branch is created from a stable point on main.
2. Final testing is performed on the release branch.
3. The tested release is delivered to customers.
4. Development of later functionality can continue on main.

This example demonstrates how a branching strategy supports parallel development without interrupting the currently working application.

### 12. Open-Source Repository Example

Large open-source repositories may receive contributions from thousands of developers. A structured branching model helps maintainers organize:

- Ongoing development on the primary branch.
- Independent feature work.
- Version-specific release branches.
- Testing and stabilization of scheduled releases.
- Fixes that must be applied to active development and supported versions.

The Kubernetes repository illustrates the same general pattern:

- A primary branch holds active integrated development.
- Separate branches may be used for feature work.
- Versioned release branches represent specific Kubernetes releases.
- Changes are tested and stabilized before being delivered.

Examining repositories such as Kubernetes, Docker, Istio, or Jenkins can help identify how large projects organize feature and release development. The exact branch names and policies may differ, but the reason for separating development, stabilization, and urgent fixes remains the same.

### 13. Branch Merge and Synchronization Rules

| Change type | Primary working branch | Required destination |
| --- | --- | --- |
| New feature | Feature branch | Main after successful testing |
| Release stabilization correction | Release branch | Release branch and main when the correction affects future development |
| Critical production correction | Hotfix branch | Relevant supported release branch and main |
| Future active development | Main or a new feature branch | Main remains the current integrated branch |

The most important consistency rule is that **main must not fall behind accepted fixes**.

### 14. Good Practices Covered

- Create a feature branch for significant or potentially breaking work.
- Allow developers to collaborate on the relevant feature branch.
- Test new functionality before merging it into main.
- Keep unrelated development out of a release branch during stabilization.
- Build customer releases from the designated release branch.
- Keep hotfix branches focused and short-lived.
- Merge production fixes into both the supported release and main.
- Return relevant release corrections to main.
- Delete temporary feature and hotfix branches after successful integration.
- Use clear branch names that describe their purpose or version.

### 15. Common Mistakes

#### Developing a large feature directly on main

This can expose incomplete or breaking work to the shared codebase. Isolate the change on a feature branch until it is ready.

#### Continuing to add features during release testing

This changes the release scope and reduces stability. Keep the release branch focused on testing and release corrections.

#### Fixing production but not updating main

The current release may work, but a future version created from main can contain the same defect. Merge the hotfix back into main.

#### Releasing from an actively changing branch

The code under test may change continuously. Create a release branch to preserve a stable release candidate.

#### Keeping temporary branches after they are no longer needed

Completed feature and hotfix branches can create confusion. Delete them after their changes have been safely integrated.

---

## Interview Questions and Answers

### 1. What is a Git branch?

A Git branch is an independent line of development created from an existing point in a repository. It allows changes to be developed and tested without immediately affecting the shared stable code.

### 2. What is a Git branching strategy?

A Git branching strategy is a defined workflow for creating, using, merging, and deleting branches for feature development, releases, and production fixes.

### 3. Why do organizations need a branching strategy?

It allows teams to work in parallel, isolate unfinished changes, stabilize releases, resolve production issues, and deliver software predictably without disrupting working functionality.

### 4. What are the four branch types in this strategy?

They are the **main or master branch**, **feature branches**, **release branches**, and **hotfix or bugfix branches**.

### 5. What is the purpose of the main branch?

The main branch holds the latest integrated and accepted code. Completed features and important fixes should eventually be synchronized with it.

### 6. What is a feature branch?

A feature branch is a temporary branch used to develop and test a new feature independently before merging it into main.

### 7. When should a feature branch be created?

It should be created when a feature is large, takes significant time, requires collaboration, or may introduce breaking changes to existing functionality.

### 8. What is the normal lifecycle of a feature branch?

It is created from main, used for development and testing, merged into main after approval, and deleted when it is no longer needed.

### 9. Can multiple feature branches exist at the same time?

Yes. Separate teams can work on different features in parallel and merge each feature into main when it is ready.

### 10. What is a release branch?

A release branch is a stable, version-specific branch used for final testing, stabilization, building, and delivering a product release.

### 11. Why create a release branch instead of releasing directly from main?

Main may continue to receive active development. A release branch freezes the intended release scope so testing can occur without unrelated new changes.

### 12. Which branch is used to deliver software to customers in this strategy?

The application is built and delivered from the appropriate release branch.

### 13. What work is performed on a release branch?

Teams perform final functional testing, end-to-end testing, stabilization, and release-specific corrections before building and shipping the product.

### 14. Can development continue after a release branch is created?

Yes. Future development can continue on main and new feature branches while the current release is stabilized separately.

### 15. What is a hotfix branch?

A hotfix branch is a short-lived branch created to correct an urgent defect in a production release.

### 16. How is a hotfix branch different from a feature branch?

A feature branch introduces planned functionality, while a hotfix branch urgently repairs a customer-facing production problem.

### 17. Where should a hotfix be merged?

It should be merged into the affected supported release branch and into main. It should also be applied to other supported release branches that contain the same defect.

### 18. Why must a hotfix be merged back into main?

Main is the source of future releases. Without the fix, a later release may reintroduce the same production defect.

### 19. Which branch should contain the latest integrated code?

The main, master, or trunk branch should contain the latest accepted and integrated changes.

### 20. Why are feature branches usually deleted after merging?

Once the work is integrated, the temporary branch has completed its purpose. Deleting it reduces confusion and keeps the repository organized.

### 21. How does branching protect existing functionality?

New or risky changes remain isolated from the stable code until development and testing have been completed successfully.

### 22. How does a branching strategy support parallel development?

Each team can work on a separate feature branch without overwriting or immediately affecting the work of other teams.

### 23. What happens when all planned features for a release are ready?

The approved features are integrated into main, a stable point is selected, and a release branch is created for final testing and delivery.

### 24. What is the difference between main and a release branch?

Main holds current integrated development, while a release branch represents a controlled version being stabilized or supported for customer delivery.

### 25. What can happen if a production fix is applied only to a release branch?

The current production version may be corrected, but main may still contain the defect, allowing it to return in a future release.

### 26. Why should unrelated features not be added to a release branch?

The branch is intended to stabilize a defined release. Adding unrelated work changes its scope and can introduce new defects during final testing.

### 27. How would you explain the complete branching workflow in an interview?

Developers create feature branches from main, test their work, and merge completed features into main. A release branch is then created from a stable point for final testing and delivery. Urgent production issues are fixed through hotfix branches, and those fixes are merged into both the supported release and main.

### 28. What names may be used for the primary development branch?

Depending on the repository, it may be called **main**, **master**, or **trunk**.

---

## Scenario-Based Interview Questions

### 1. A team must add percentage calculations to a working calculator. The change is large and may break existing operations. What should it do?

Create a dedicated feature branch from the current main branch. Develop and test the percentage functionality there, verify that existing calculations still work, and merge the branch into main only after successful validation.

### 2. Two teams need to develop percentage and exponent features simultaneously. How should the work be organized?

Create separate feature branches for each feature. Both teams can work independently, and each branch can be tested and merged into main when its feature is ready.

### 3. A planned release is undergoing end-to-end testing, but developers must begin work on the next version. How can both activities continue safely?

Create a release branch for the version under test. Stabilization can continue on that branch while new development proceeds on main and separate feature branches.

### 4. A critical defect is reported three days after a production release. What branching process should be followed?

Create a short-lived hotfix branch for the affected release, implement and test the correction, merge it into the supported release branch, deliver the corrected build, and merge the same fix into main.

### 5. A hotfix was merged into the release branch but not into main. What is the risk?

The current release is corrected, but main still contains the defect. A future release created from main may reintroduce the same issue. The hotfix must also be merged into main.

### 6. A feature is complete, but its testing is not finished. Should it be merged into main?

No. The feature should remain isolated on its branch until the team is confident that it works correctly and does not break existing functionality.

### 7. Developers keep adding new features to a branch while the release team is testing it. What should be changed?

Create or use a dedicated release branch with a controlled scope. New feature development should continue on main or feature branches instead of entering the release under stabilization.

### 8. An application supports several customer versions, and a critical defect affects more than one supported release. Where should the fix go?

Apply the tested hotfix to every supported release branch affected by the defect and merge it into main so future versions also contain the correction.

### 9. A completed feature branch has already been merged successfully. What should happen to the branch?

After confirming that the changes are safely integrated, delete the temporary feature branch to keep the repository clear and manageable.

### 10. A product manager requests bike-booking functionality while the existing cab-booking system must remain stable. How should the team proceed?

Keep cab-related development on the existing workflow and create a feature branch for bike bookings. Develop and test the new functionality independently, then merge it into main when both old and new functionality work correctly.

### 11. A team is ready to deliver version 3, but main already contains unfinished work intended for version 4. What should it do?

Version 3 should be built from its stable release branch rather than the actively changing main branch. The release branch preserves the tested version 3 scope.

### 12. A correction is discovered during release stabilization and will also be required in future versions. How should it be handled?

Apply and test the correction on the release branch, then merge or reproduce the accepted correction in main so the active codebase remains current.

---

## Quick Revision Notes

- A **branch** is an independent line of development.
- A **branching strategy** defines how branches are created, used, merged, and deleted.
- Branching isolates risky or incomplete work from stable code.
- **Main, master, or trunk** holds the latest integrated and accepted code.
- **Feature branches** isolate planned functionality.
- Feature branches are merged into main after development and testing.
- Temporary feature branches can be deleted after successful integration.
- **Release branches** freeze a selected version for stabilization and delivery.
- Functional and end-to-end testing are performed on the release branch.
- In this strategy, customer builds are produced from release branches.
- Development can continue on main while a release branch is being tested.
- **Hotfix branches** address urgent production defects.
- Hotfix branches are normally very short-lived.
- A hotfix must reach the affected release branch and main.
- Apply a hotfix to other supported release branches when they contain the same defect.
- Relevant release corrections must return to main.
- Multiple feature branches allow teams to work in parallel.
- Clear branch separation supports stable and predictable releases.

---

## Key Terms and Definitions

| Term | Definition |
| --- | --- |
| **Branch** | An independent line of development created from an existing repository state. |
| **Branching strategy** | A defined process for managing branches throughout development, testing, release, and production support. |
| **Main branch** | The central branch that holds the latest integrated and accepted code. |
| **Master branch** | A traditional alternative name for the primary branch. |
| **Trunk** | Another term used for the primary development line in some projects. |
| **Feature branch** | A temporary branch used to develop and test a specific new feature. |
| **Release branch** | A version-specific branch used for final testing, stabilization, building, and delivery. |
| **Hotfix branch** | A short-lived branch used to resolve an urgent production defect. |
| **Bugfix branch** | A branch used to correct a defect; in the discussed workflow, it may refer to an urgent hotfix branch. |
| **Merge** | The process of integrating changes from one branch into another. |
| **Active development** | Ongoing work in which new features and fixes continue to be added. |
| **Breaking change** | A change that may disrupt or alter existing application behavior. |
| **Release stabilization** | Final testing and correction of a selected software version before delivery. |
| **Functional testing** | Validation that individual application functions behave as required. |
| **End-to-end testing** | Validation of complete workflows across the application. |
| **Supported release** | A released product version that still receives maintenance or production fixes. |
| **Branch synchronization** | Ensuring that accepted changes, especially fixes, are propagated to every branch that requires them. |

---

## Important Commands

No commands covered in this session.

---

## Key Takeaways

- A branching strategy separates feature development, release preparation, and urgent production maintenance.
- Main must remain the current integrated source for future development.
- Large or breaking changes should be developed and tested on feature branches.
- A release branch provides a controlled version for final testing and customer delivery.
- Production hotfixes must be applied to the affected supported release and merged into main.
- Correct branch synchronization prevents fixed defects from returning in later versions.
- A consistent branching workflow helps teams collaborate safely and deliver releases predictably.
