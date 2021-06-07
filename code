% Pławiak, Paweł (2017), “ECG signals (1000 fragments)”, Mendeley Data, V3, doi: 10.17632/7dybx7wyfn.3
ECG = val;
figure(1)
subplot(3,1,1)
plot(ECG(1000:2000))

%low pass filter design
fs=360; %sampling rate
filter_order=10; %ordering the filter
cut_of_frequency=18;
[a,b]=butter(filter_order,(cut_of_frequency/(fs/2)),'low');

%high pass filter design
fs=360; %sampling rate
filter_order=10; %ordering the filter
cut_of_frequency=4; 
[a,b]=butter(filter_order,(cut_of_frequency/(fs/2)),'high');

%plotting the frequency response
[h,w]=freqz(a,b);
figure(2);
subplot(2,1,1)
plot(w/pi*fs/2,abs(h),'-');
title('low pass magnitude response');
grid on

%plotting the frequency response
[h,w]=freqz(a,b);
figure(2);
subplot(2,1,2)
plot(w/pi*fs/2,abs(h),'-');
title('high');
grid on

%applying low pass filter
EEGhighpass=filter(a,b,ECG);
figure(1)
subplot(3,1,2)
plot(EEGhighpass(1000:2000))
title('noise removed')


%apply high pass filter
filteredEEG=filter(a,b,EEGhighpass);
figure(1)
subplot(3,1,3)
plot(filteredEEG(1000:2000))
title('movement artifits removed');

%localizing R-waveforms
[pks, locs] = findpeaks(filteredEEG(1801:end));
threshold = 2*rms(filteredEEG(1801:end));  %esik belirliyoruz
Rwave = pks>threshold; %bu esigi asan peakler r waveler
R_waveform= zeros(size(filteredEEG(1801:end)));
R_waveform(locs(Rwave))= max(filteredEEG(1801:end));
figure(3)
plot(filteredEEG(1801:end));
hold on
stem(R_waveform,'r','')
title('Location of R-wave of the input ECG')

%%heart rate calculation
total_number_beat= sum(Rwave);
heart_rate= (total_number_beat/5)*60;
display(heart_rate)
