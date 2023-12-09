clear all
a = arduino();
cam = webcam('Logi C270 HD WebCam');
cam1 = webcam('Logi C270 HD WebCam');

a
shield = addon(a,'Adafruit\MotorShieldV2');
dcm = dcmotor(shield,1);
dcm1 = dcmotor(shield, 3);
dcm3 = dcmotor(shield, 2);
dcm4 = dcmotor(shield, 4);
iteration = 0;
maxIterations = 100;

isFoundR = 0;
isReached = 0;
while(true)
    % iteration = iteration + 1;

    % Capture the frame
    RGB = snapshot(cam);

    % Convert to HSV
    I = rgb2hsv(RGB);

    % Adjust threshold values based on your requirements
    channelr1Min = 0.0;
    channelr1Max = 0.05;

    channelr2Min = 0.5;
    channelr2Max = 1.0;

    channelr3Min = 0.5;
    channelr3Max = 1.0;

    channelg1Min = 0.22;
    channelg1Max = 0.39;

    channelg2Min = 0.5;
    channelg2Max = 1.0;

    channelg3Min = 0.5;
    channelg3Max = 1.0;

    channelb1Min = 0.56;
    channelb1Max = 0.68;

    channelb2Min = 0.5;
    channelb2Max = 1.0;

    channelb3Min = 0.5;
    channelb3Max = 1.0;

    % Create binary mask
    sliderRBW = (I(:, :, 1) >= channelr1Min & I(:, :, 1) <= channelr1Max) & ...
               (I(:, :, 2) >= channelr2Min & I(:, :, 2) <= channelr2Max) & ...
               (I(:, :, 3) >= channelr3Min & I(:, :, 3) <= channelr3Max);

    sliderGBW = (I(:, :, 1) >= channelg1Min & I(:, :, 1) <= channelg1Max) & ...
               (I(:, :, 2) >= channelg2Min & I(:, :, 2) <= channelg2Max) & ...
               (I(:, :, 3) >= channelg3Min & I(:, :, 3) <= channelg3Max);

    sliderBBW = (I(:, :, 1) >= channelb1Min & I(:, :, 1) <= channelb1Max) & ...
               (I(:, :, 2) >= channelb2Min & I(:, :, 2) <= channelb2Max) & ...
               (I(:, :, 3) >= channelb3Min & I(:, :, 3) <= channelb3Max);

    % Find connected components
    CCR = bwconncomp(sliderRBW);
    sR = regionprops(CCR, 'Centroid', 'Area');

    CCG = bwconncomp(sliderGBW);
    sB = regionprops(CCG, 'Centroid', 'Area');

    CCB = bwconncomp(sliderBBW);
    sG = regionprops(CCB, 'Centroid', 'Area');

    % Display results
    
    [nRx, nRy] = size(sliderRBW);
    cenR = round([nRx, nRy] / 2);
    
       
        
        
    
        % figure(2);
        % imshow(sliderGBW);
        % 
        % figure(2);
        % imshow(sliderBBW);
    
    if (~isempty(sR))
        % Find the centroid of the largest area
        areasR = cat(1, sR.Area);
        [maxAreaR, indR] = max(areasR);
        centroidsR = cat(1, sR.Centroid);
        if isFoundR == 0
            figure(1);
            imshow(RGB);
            hold on
        else
            analog3 = readVoltage(a, 'A1')*(1023/3);
            while (analog3 > 395)
                RGB = snapshot(cam);
                start(dcm3);
                dcm3.Speed = -0.2;
                analog3 = readVoltage(a, 'A1')*(1023/3);
                disp(analog3);
                figure(1);
                imshow(RGB);
                hold on;
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off;
                figure(2);
                imshow(sliderRBW);
                hold on
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off
            end
            stop(dcm3);
            % analog4 = readVoltage(a, 'A3')*(1023/3);
            for i = 1:50
                start(dcm4);
                dcm4.Speed = 0.3;
                RGB = snapshot(cam);
                % analog4 = readVoltage(a, 'A3')*(1023/3);
                % disp(analog4);
                figure(1);
                imshow(RGB);
                hold on;
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off;
                figure(2);
                imshow(sliderRBW);
                hold on
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off
            end
            stop(dcm4);
            while (analog3 < 650)
                RGB = snapshot(cam);
                start(dcm3);
                dcm3.Speed = 0.2;
                analog3 = readVoltage(a, 'A1')*(1023/3);
                disp(analog3);
                figure(1);
                imshow(RGB);
                hold on;
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off;
                figure(2);
                imshow(sliderRBW);
                hold on
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off
            end
            stop(dcm3);

            for i = 1:50
                start(dcm4);
                dcm4.Speed = -0.3;
                % analog4 = readVoltage(a, 'A3');
                RGB = snapshot(cam);
                figure(1);
                imshow(RGB);
                hold on;
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off;
                figure(2);
                imshow(sliderRBW);
                hold on
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off
            end
            stop(dcm4);
            isFoundR = 0;
            isReached = 1;
            for i = 1:20
                RGB = snapshot(cam);
                figure(1);
                imshow(RGB);
                hold on;
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off;
                figure(2);
                imshow(sliderRBW);
                hold on
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off
            end
            pause(2);
            disp("stops here");
            RGB = snapshot(cam);
        
            % Convert to HSV
            I = rgb2hsv(RGB);
            sliderRBW = (I(:, :, 1) >= channelr1Min & I(:, :, 1) <= channelr1Max) & ...
                       (I(:, :, 2) >= channelr2Min & I(:, :, 2) <= channelr2Max) & ...
                       (I(:, :, 3) >= channelr3Min & I(:, :, 3) <= channelr3Max);
            % Find connected components
            CCR = bwconncomp(sliderRBW);
            sR = regionprops(CCR, 'Centroid', 'Area');
            areasR = cat(1, sR.Area);
            [maxAreaR, indR] = max(areasR);
            centroidsR = cat(1, sR.Centroid);
            figure(1);
            imshow(RGB);
            hold on
            pause(2);
            disp("fucck");
            stop(dcm);
            stop(dcm1);
            stop(dcm3);
            stop(dcm4);
        end
        % disp("R");
        % disp(centroidsR);
        if (~isempty(centroidsR) && isFoundR == 0)
            if(centroidsR(indR, 2) > 270 )
                disp("1");
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32)
                hold off;
                figure(2);
                imshow(sliderRBW);
                hold on
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off
                start(dcm);
                dcm.Speed = -0.2;
            elseif(centroidsR(indR, 2) < 210)
                disp("2");
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off;
                figure(2);
                imshow(sliderRBW);
                hold on
                plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                hold off
                start(dcm);
                dcm.Speed = 0.2;
            elseif(centroidsR(indR, 2) >= 210 && centroidsR(indR, 2) <= 270)
                stop(dcm);
                %dcm.speed = 0.0;
                if(centroidsR(indR, 1) > 330 )
                    disp("3");
                    plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                    hold off;
                    figure(2);
                    imshow(sliderRBW);
                    hold on
                    plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                    hold off
                    start(dcm1);
                    dcm1.Speed = -0.2;
                elseif(centroidsR(indR, 1) < 290)
                    disp("4");
                    plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                    hold off;
                    figure(2);
                    imshow(sliderRBW);
                    hold on
                    plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                    hold off
                    start(dcm1);
                    dcm1.Speed = 0.2;
                elseif(centroidsR(indR, 1) >= 290 && centroidsR(indR, 1) <= 330)
                    disp("5");
                    plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                    hold off;
                    figure(2);
                    imshow(sliderRBW);
                    hold on
                    plot(centroidsR(indR, 1), centroidsR(indR, 2), 'm*', 'MarkerSize', 32);
                    hold off
                    stop(dcm1);
                    isFoundR = 1;   
                    isReached = 0; 
                end
            end
        end
    else
        figure(1);
        imshow(RGB);
        figure(2);
        imshow(sliderRBW);
    end

    % Add a pause to avoid rapid display updates (optional)
    % pause(0.1);
end

% Release the webcam
% clear cam;
