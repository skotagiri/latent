# latent 

## Introduction
`latent`  is a framework for simulating impact of network conditions and Adaptive Bitrate Manifest 
engineering on Quality of Experience. I got curious about how DASH/HLS/SmoothStreaming 
VOD manifest designs impact the load times and buffering times for streaming media playback 
and how the decisions made to construct such manifests and the corresponding heuristics can affect 
media playback.

## Background
This application takes empirical approach to computing the estimated QoE for users based on several
variables such as the choice of steps on ABR Ladder, per-title encoding optimization etc. The main
reason for choosing the empirical approach to modelling is to make it more intuitive for non data-scientists
to understand the impact of several inter-related parameters. 

For a robust OTT streaming service, there are several systems that contribute to the cost of delivering
media to customers. They are broken down to two lifecycles. 

### Asset Journey
In this lifecycle, the costs are incurred for each title that appears in the catalog. This model does not
assume the cost of actual content production. Only that a "Program" is ready to be added to the catalog.

So for each minute of "Program" in the catalog, the costs associated are

| Cost                                   | Type         |
|----------------------------------------|--------------|
| Generating/Transporting mezzanine      | Fixed        |
| Storing mezzanine                      | Recurring    |
| Transcoding Mezzanine to ABR Ladder    | Fixed        |
| Storage costs for Packaged ABR Content | Recurring    |

### User Journey
For the user journey lifecycle, the costs associated media file are related to the users actually consuming
the generated ABR packages. One would assume that more users views will provide more revenue to the providers 
and as such a thing to be encouraged. Regardless of the hypothetical revenue, there are real costs associated 
with this streaming both to the provider and to the user.

For each "playback session", the following costs apply.

| Cost               | Bearer   | 
|--------------------|----------|
| CDN Cache Width    | Provider |
| CDN Egress Costs   | Provider |
| Internet Bandwidth | User     |

