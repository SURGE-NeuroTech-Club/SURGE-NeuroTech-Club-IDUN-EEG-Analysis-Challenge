# IDUN-EEG-Analysis-Challenge

This is the codebase for the SURGE Neurotech club Kaggle competition - ["BCI-I & IDUN EEG Analysis Challenge"](https://www.kaggle.com/competitions/bci-i-idun-eeg-analysis-challenge/overview)

## Introduction

This challenge invites you to explore the fascinating world of sleep science using real EEG data collected with IDUN Guardian Earbuds. The goal is to develop machine learning models that can accurately classify sleep events from EEG data.

Sleep analysis offers unique insights into memory, cognition, and health, with broad implications for neuroscience and neurotechnology. In this challenge, you'll receive EEG data from multiple subjects annotated with sleep-related events markers such as sleep spindles, K-complexes, and REM stage. You goal is to develop a machine learning model that can learn to detect these events in the EEG signal, and that can be used to analyze EEG data from new subjects to gain insights into sleep and health. Whether you're a seasoned ML expert or new to EEG analysis, this is a fantastic opportunity to contribute to neurotechnology while building practical skills in EEG data processing and classification. If you're interested in the intersection between machine learning and neurotech, this is the right challenge for you!

Read more about the BCI Initiative (https://bci-i.github.io/) and IDUN (https://iduntechnologies.com/)


## Description

### Dataset Overview

The dataset for this competition contains EEG data from four subjects, with the following split:

**Training Set:** Data from three subjects, includes time-series EEG recordings and corresponding event labels.
**Test Set:** Data from one subject, includes time-series EEG recordings, but does not include event labels. Event labels for the test subject are held out and used to evaluate model quality.

### Data Collection

The EEG data was collected using the IDUN Guardian Earbuds (see also this whitepaper), a wearable EEG device with in-ear dry electrodes. Each subject's data includes continuous EEG signals recorded overnight while the subjects slept. The sampling rate of the data is 250 Hz, with filtering applied between 0.75 and 35 Hz (we refer to this as raw EEG data despite this filtering - participants are encouraged to explore additional pre-processing steps).

The IDUN Guardian Earbuds is a single-channel in-ear EEG device that allows for prolonged monitoring of sleep-related neural activity with minimal disruption for the subjects. For this challenge, a second EEG system, with more recording channels, was used as a ground truth to confirm that events detected in the Guardian signal are correct. We only provide data from the IDUN Guardian.
Recordings were analyzed to manually identify the onset of various sleep and wake related neural activity signals (e.g., around REM sleep onset).

### Task Description

You will be provided with EEG data segmented into 30-second epochs. Each epoch is aligned to the onset of one sleep event marker (see below). Your goal is to develop a machine learning model that, given a 30s EEG epoch as input can predict the event marker associated with it.

Note that you're given labels for the three train subjects only. You will need to use these to train an algorithm that can then transfer to the test subject, for whom you don't have any supervised data. The aim is to develop models that could work for any new subject without requiring additional training.

Transfer learning is a challenging but well-studied topic in machine learning. You can implement some of the algorithms described in the literature or develop your own! There are 7 marker types so you will need to explore various approaches to multi-class classification while considering data preprocessing strategies for EEG data.

### Data Composition

**Epochs:** Data is segmented into 30-second epochs. Each epoch corresponds to a specific sleep event (if any), such as sleep spindles, K-complexes, or REM sleep.
**Labels:** Each epoch has a label which indicates the sleep event associated to it. Labels are provided as "strings"
with the event marker (see below).

**Events (Markers)**

The seven possible sleep events in the dataset are:
> SS: Sleep Spindles
> K: K-Complexes
> REM: Rapid Eye Movements
> Son: Sleep Onset
> Soff: Sleep Offset
> A: Arousals
> MS: Microsleep


**Continuous EEG data:** we provide data cut into epochs for convenience. The final submission for this challenge will have to be made using data organized into epochs. However, we also provide the "un-cut" data (continuous EEG recording over an entire night and associated markers timestamps). This is intended to be used by participants wishing to apply pre-processing steps to the EEG data that don't work well with data already cut into epochs. We have example code here showing how to organize the continuous EEG data into epochs for fitting ML models and preparing a submission file.

### Baseline Models and Code

To help participants get started, we provide:

Starter code for data exploration, preprocessing guidance, and visualization of the class distributions.
Baseline models to give you a sense of initial performance, some of the main pitfalls in approaching this challenge and inspire your model development.
Detailed instructions on how to prepare and format your submission.
Check out the example code here.

Feel free to experiment with preprocessing techniques, feature extraction, and model optimization to create an effective classification pipeline.

### Metric

Given the dataset’s class imbalance, this competition uses the Weighted F1-Score as the primary evaluation metric. The Weighted F1-Score emphasizes the importance of both precision and recall across classes, providing a balanced assessment of model performance, especially on underrepresented classes.

### Submission File

You will need to provide a submission .csv file. We've provided detailed instructions on how to prepare this data in the tutorials linked above. Your submission file should have as many rows as there are epochs in the test dataset. Each row should have an ID (the epoch's number in the dataset, starting at 0) and a TARGET, a string with the marker's name predicted by your model.

> ID,Marker
1,REM
2,K
3,A
etc...

# Resources:

- Repository made by challenge-creators: https://github.com/BCI-I/BCII-IDUN-Challenge-tutorials
- Link to the Kaggle challenge page: https://www.kaggle.com/competitions/bci-i-idun-eeg-analysis-challenge/overview