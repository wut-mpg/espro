---
layout: task
title: Windowed transform
category: lab
lab: 4
task: 2
brief: Using STFT to analyze signals changing in time
---

{% comment %} https://www.freesound.org/s/177268/ {% endcomment %}

## Wprowadzenie

Signals that are not periodic (e.g. speech) are hard to analyze using whole recording to calculate fft. To distinguish particular parts of the speech, words and even single phonems, one has to apply Fourier transform to smaller fragments of the recording. Input signal can be split into short windows, and for each of them different fft can be calculated. Windows can have length appropriate to the application (shorter if we want to detect small events) or longer (if we need better frequency resolution). Final result can be presented in the form of a spectrogram.

## Calculating spectrograms



Download sample [audio file]({{ site.baseurl }}/public/l2/funf.wav) and load it ([audioread](https://www.mathworks.com/help/matlab/ref/audioread.html)). 
It is a single word (*fünf*) recorded.

{% highlight matlab %}
% x - recorded samples
% Fs - sampling rate
[x, Fs] = audioread('funf.wav');
{% endhighlight %}

![]({{ site.baseurl }}/public/l2/funf.png)

After loading the file calculate and show the [spectrogram](https://www.mathworks.com/help/signal/ref/spectrogram.html). Manipulate the parameters (window size, overlap) and observe the differences in the result.

{% highlight matlab %}
% x - signal
% 128 - window size
% 64 - window overlap
% [] - number of FFT points per window (default)
% Fs - sampling rate
% 'yaxis' - put frequency on y axis, time on x
spectrogram(x, 128, 64, [], Fs, 'yaxis');
{% endhighlight %}

![]({{ site.baseurl }}/public/l2/s_16.png)
![]({{ site.baseurl }}/public/l2/s_256.png)
![]({{ site.baseurl }}/public/l2/s_1024.png)


## Ultrasonic sensor analysis

One of the methods for obstacle detection (and distance measurement in general) is using ultrasonic sensors (so called *ping* sensors). They send short burst of high frequency *pings* and detect echo reflected by obstacles. By calculating the time from sending ping to receiving it the distance can be measured.

For sensor sending 8 1ms pings (with 40kHz base frequency) calculate the distance to the obstacle from registered echo recording. Use [simulated sample]({{ site.baseurl }}/public/l2/output.txt). Recording has 200kHz sampling rate.

*Ping* signal:
![]({{ site.baseurl }}/public/l2/4_1.png)
![]({{ site.baseurl }}/public/l2/4_2.png)

Registered *echo*:
![]({{ site.baseurl }}/public/l2/4_3.png)

Calculate spectrogram for the recording, find the echo location and calculate the signal travel time. From it calculate the distance. Assume speed of sound to be 343 *m/s*.