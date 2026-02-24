# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN

## AIM: 
To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
```
clc;
close;

wp = input('Enter pass band frequency (radians) = ');
ws = input('Enter stop band frequency (radians) = ');
alphap = input('Enter pass band attenuation (dB) = ');
alphas = input('Enter stop band attenuation (dB) = ');
T = input('Enter sampling time = ');

omegap = (2/T)*tan(wp/2);
omegas = (2/T)*tan(ws/2);

N = ceil( log10((10^(0.1*alphas)-1)/(10^(0.1*alphap)-1)) / ...
          (2*log10(omegas/omegap)) );
          
omegac = omegap / ((10^(0.1*alphap)-1)^(1/(2*N)));

hs = analpf(N,'butt',[0,0],omegac);

z = poly(0,'z');
Hz = horner(hs,(2/T)*((z-1)/(z+1)));

HW = frmag(Hz,512);
w = 0:%pi/511:%pi;

plot(w/%pi,abs(HW));
xlabel('Normalized Digital Frequency');
ylabel('Magnitude');
title('Frequency Response of Butterworth IIR LPF');

```


## PROGRAM (HPF): 
```
clc; 
clear;
close;

wp = input('Enter wp (Radians)= ');
ws = input('Enter ws (Radians)= ');
alphap = input('Enter passband attenuation (dB)= ');
alphas = input('Enter stopband attenuation (dB)= ');
T = input('Enter Sampling Time= ');

omegap = (2/T)*tan(wp/2);
omegas = (2/T)*tan(ws/2);
disp(omegap,'omegap=');
disp(omegas,'omegas=');

N = ceil(log10((10^(0.1*alphas)-1)/(10^(0.1*alphap)-1)) / ...
        (2*log10(omegap/omegas)));
disp(N,'Order N=');

omegac = omegas/((10^(0.1*alphas)-1)^(1/(2*N)));
disp(omegac,'omegac=');

hs = analpf(N,'butt',[0 0],omegac);
disp('Analog LPF H(s)='); disp(hs);

s = poly(0,'s');
hs_hp = horner(hs,(omegac^2)/s);
disp('Analog HPF H(s)='); disp(hs_hp);

z = poly(0,'z');
Hz = horner(hs_hp,(2/T)*(z-1)/(z+1));
disp('Digital HPF H(z)='); disp(Hz);

HW = frmag(Hz,512);
w = linspace(0,%pi,512);
plot(w/%pi,abs(HW));
xlabel('Normalized Frequency (×π rad/sample)');
ylabel('Magnitude');
title('Butterworth IIR High-pass Filter');
xgrid();
```

## OUTPUT (LPF) : 
<img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/3047f66d-228d-4a16-b1e6-ef0477d53dc3" />

## OUTPUT (HPF) : 
<img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/fd6cfce4-e0a2-4a93-a396-01146fe80dd1" />

## RESULT: 
Thus, design of Butterworth Low pass and High pass IIR filter waveforms were plotted and output was verified.
