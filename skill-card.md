## Description: <br>
Yzl Aiot lets agents read YZL-AIoT sensor data and send control commands to supported cloud-connected devices through the YZL open API. <br>

This skill is ready for commercial/non-commercial use. <br>

## Publisher: <br>
[yzlkj](https://clawhub.ai/user/yzlkj) <br>

### License/Terms of Use: <br>
MIT-0 <br>


## Use Case: <br>
External users and device operators use this skill to inspect YZL-AIoT device status, retrieve soil moisture, temperature, level, and history data, and issue authorized control commands such as opening or closing supported valves. <br>

### Deployment Geography for Use: <br>
Global <br>

## Known Risks and Mitigations: <br>
Risk: The skill can directly open or close real valves from broad natural-language commands without a confirmation step. <br>
Mitigation: Use it only with API keys scoped to authorized devices, verify the target device before issuing commands, and require operator confirmation for valve actions. <br>
Risk: A broadly scoped YZLIOT_API_KEY could allow unintended access to sensor data or physical device control. <br>
Mitigation: Store the API key only in the runtime environment and use the least-privileged key available for the intended device set. <br>
Risk: Exceeding the YZL open API rate limits (for example 6 requests / 30 s for history, 2 requests / 5 s for commands, concurrency 2) or repeatedly returning non-zero status codes from the same IP can trigger the platform's automatic protection and a PERMANENT IP ban. <br>
Mitigation: Keep every request rate strictly below the published limits, never exceed concurrency 2, use exponential backoff (1s/2s/4s) instead of retrying in a burst, and ensure the API key is valid to avoid repeated 401 responses. <br>
Risk: Polling loops that re-query full device details can multiply requests against the device detail endpoint. <br>
Mitigation: Use `/open/device/all` with `latestModificationTime` for incremental sync first, then fetch details only for changed devices, and keep polling intervals at 5/10/30 minutes. <br>


## Reference(s): <br>
- [ClawHub release page](https://clawhub.ai/yzlkj/yzl-aiot) <br>
- [YZL open API endpoint](https://open.yzlkj.com) <br>
- [YZL open API documentation](https://cn6l1w4yn0.apifox.cn) <br>
- [YZL official website](https://www.yzlkj.com) <br>
- Contact: 089836692518 / 18689850608 <br>


## Skill Output: <br>
**Output Type(s):** [Text, Shell commands, Guidance] <br>
**Output Format:** [Plain text and Markdown with inline shell commands] <br>
**Output Parameters:** [1D] <br>
**Other Properties Related to Output:** [Requires Python 3 (run with `python`, or `python3` where only that exists) and YZLIOT_API_KEY; outputs may reflect live device state and command results.] <br>

## Skill Version(s): <br>
1.2.1 (source: server release metadata and artifact _meta.json) <br>

## Ethical Considerations: <br>
Users should evaluate whether this skill is appropriate for their environment, review any generated or modified files before relying on them, and apply their organization's safety, security, and compliance requirements before deployment. <br>
