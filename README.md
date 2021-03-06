# Atrial Fibrillation Detection
Each file in the top level of the source code (not mcode.m and and wfdb...) is executable as a script. 
AFDetectionV2 is the final algorithm, with several parameters at the beginning. The parameters are described below:

mV = Gradient cutoff for R-wave drop off. A higher value will result in more strict R-wave Detection. Value should be reduced if sampling rate is above 128.
rWaveCutoff = Minimum gradient R-wave must rise above to be considered. Can be increased/decreased depending on signal quality. 
p_wave_window_start = How far to look behind R-wave for P-wave. Increasing can improve chances of finding a P-wave, but 200ms is a maximum. 

lead = if signal comes with multiple lead values, we must choose a specific lead to analyse.

butterworth = If true, a Butterworth Highpass Filter is used to remove Baseline wander.
powerNoiseRemoval = If true, a Butterworth Notch Filter is used to remove Powerline Interference.

windowSize = The amount of signal considered at any one time for AF detection. Decreasing increases sensitivity but reduces specificity. 
    Increasing decreases sensitivity but increases specificity.  
signalStart = parameter to choose where to start looking at the signal (in seconds). 
signalTime = amount of signal to download (in seconds)

sDev_threshold = SDSD threshold the window must go above to be classed as AF
p_score_threshold = Average pscore threshold window must go above to be classed as AF

plotAllWindows = If True, every window is plotted. Not recommended for signalTime > 60
plotAFWindows = If True, every window classified as AF is plotted. 

When all parameters are chosen, remove the comment brackets from either Training or Testing data, and run the script, e.g:

%{ <---- remove this
signalCode = 'nsrdb/16265'; 
[s,Fs,t]=rdsamp(signalCode,[], 250*1); % Load 1 second to get sample rate
signalStart = 1*Fs;
%} <---- remove this

The algorithm is subject to the availability of signals from PhysioBank. That is, if PhysioBank is down, the 
algorithm will not be able to be run due to having no data. 
