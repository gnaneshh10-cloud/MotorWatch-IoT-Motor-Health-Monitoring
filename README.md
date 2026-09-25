# MotorWatch-IoT-Motor-Health-Monitoring
An IoT-based smart system that monitors motor health in real time using sensors, Arduino, ESP32, and Machine Learning, with a web dashboard for condition and risk monitoring.
**MotorPulse – Smart Condition Monitoring**  
**1\. Introduction**  
MotorPulse is an IoT-based smart condition monitoring system designed to monitor motor health in real time. The system combines sensors, Arduino UNO, ESP32, Flask backend, and Machine Learning to identify abnormal motor conditions.  
**2\. Objective**  
The main objective of MotorPulse is to continuously monitor motor-related parameters, detect abnormal conditions, and display the motor health status through a web dashboard.  
**3\. System Architecture**  
Sensors → Arduino UNO → ESP32 → Flask Backend → Random Forest ML → Web Dashboard  
**4\. Hardware Components**  
Arduino UNO  
ESP32  
IR Sensor  
Rain Sensor  
LDR Sensor  
LCD Display  
Buzzer  
Voltage Divider  
**5\. Software & Technologies**  
Arduino IDE  
Embedded C/C++  
Python  
Flask  
HTML/CSS  
Machine Learning  
Random Forest Algorithm  
**6\. Schematic diagram**  
![](DIAGRAM.png)


**7\. Block Diagram**
![](BLOCK.jpg)


Working

1. Sensors collect motor and environmental data.
2. Arduino UNO reads and processes the sensor values.
3. ESP32 receives the data and sends it through Wi-Fi.
4. Flask backend receives and processes the data.
5. Random Forest analyzes the input features.
6. The web dashboard displays the motor condition, risk, and confidence.

Output

The system provides:

- Motor RPM
- Rain Status
- Light Status
- Alarm Status
- Machine Condition
- ML Prediction
- Risk Percentage
- Confidence Percentage

Future Scope

- Predictive maintenance
- Cloud data storage
- Mobile application
- More sensors for advanced motor monitoring
- Real-time alerts

  
Final Result
![](PRODUCT.jpg)

Challebody {nge 

The major challenges were sensor accuracy, hardware integration, real-time data transmission and Machine Learning prediction

Solution 

Sensor readings-ah calibrate panni, multiple readings-ah average eduthu accurate monitoring achieve pannom.

Coding
<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <title>Industrial Machine Health Monitoring</title>


    <style>

        /* ================= GLOBAL ================= */

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            background: #eef1f5;
            color: #1f2937;
        }


        /* ================= HEADER ================= */

        header {
            background: #111827;
            color: white;
            padding: 25px;
            text-align: center;
        }

        header h1 {
            font-size: 30px;
            margin-bottom: 8px;
        }

        header p {
            color: #cbd5e1;
            font-size: 15px;
        }


        /* ================= MAIN ================= */

        .container {
            max-width: 1200px;
            margin: 30px auto;
            padding: 0 20px;
        }


        /* ================= MACHINE STATUS ================= */

        .status-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            margin-bottom: 25px;

            box-shadow:
                0 5px 15px rgba(0,0,0,0.08);
        }

        .status-card h2 {
            margin-bottom: 15px;
        }

        #machineStatus {
            display: inline-block;
            padding: 12px 35px;
            border-radius: 30px;
            font-size: 22px;
            font-weight: bold;
        }

        .healthy {
            background: #dcfce7;
            color: #166534;
        }

        .warning {
            background: #fef3c7;
            color: #92400e;
        }

        .critical {
            background: #fee2e2;
            color: #991b1b;
        }

        .disconnected-status {
            background: #e5e7eb;
            color: #374151;
        }


        /* ================= CONNECTION ================= */

        .connection {
            background: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            margin-bottom: 25px;

            box-shadow:
                0 5px 15px rgba(0,0,0,0.08);
        }

        #connectionStatus {
            font-weight: bold;
        }

        .connected {
            color: #16a34a;
        }

        .disconnected {
            color: #dc2626;
        }


        /* ================= SENSOR CARDS ================= */

        .sensor-grid {
            display: grid;

            grid-template-columns:
                repeat(3, 1fr);

            gap: 20px;

            margin-bottom: 25px;
        }

        .sensor-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            text-align: center;

            box-shadow:
                0 5px 15px rgba(0,0,0,0.08);

            transition: 0.2s;
        }

        .sensor-card:hover {
            transform: translateY(-3px);
        }

        .sensor-icon {
            font-size: 40px;
            margin-bottom: 10px;
        }

        .sensor-card h3 {
            margin-bottom: 12px;
        }

        .sensor-value {
            font-size: 30px;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .sensor-unit {
            color: #6b7280;
        }


        /* ================= ML CARD ================= */

        .ml-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;

            box-shadow:
                0 5px 15px rgba(0,0,0,0.08);
        }

        .ml-card h2 {
            margin-bottom: 25px;
        }

        .ml-grid {
            display: grid;

            grid-template-columns:
                repeat(3, 1fr);

            gap: 20px;

            text-align: center;
        }

        .ml-box {
            background: #f8fafc;
            padding: 20px;
            border-radius: 12px;
        }

        .ml-box h3 {
            font-size: 15px;
            color: #64748b;
        }

        .ml-box p {
            margin-top: 10px;
            font-size: 25px;
            font-weight: bold;
        }


        /* ================= SENSOR ANALYSIS ================= */

        .analysis-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;

            box-shadow:
                0 5px 15px rgba(0,0,0,0.08);
        }

        .analysis-card h2 {
            margin-bottom: 20px;
        }

        .parameter {
            margin-bottom: 20px;
        }

        .parameter-title {
            display: flex;
            justify-content: space-between;
            margin-bottom: 7px;
            font-weight: bold;
        }

        .bar {
            width: 100%;
            height: 18px;
            background: #e5e7eb;
            border-radius: 20px;
            overflow: hidden;
        }

        .bar-fill {
            height: 100%;
            width: 0%;
            transition: width 0.5s ease;
        }

        #motionBar {
            background: #2563eb;
        }

        #lightBar {
            background: #f59e0b;
        }

        #rainBar {
            background: #06b6d4;
        }


        /* ================= ALERT ================= */

        #alertBox {
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            margin-bottom: 25px;
            display: none;
        }

        #alertBox h2 {
            margin-bottom: 10px;
        }

        .alert-warning {
            background: #fef3c7;
            color: #92400e;
        }

        .alert-critical {
            background: #fee2e2;
            color: #991b1b;
        }


        /* ================= FOOTER ================= */

        footer {
            background: #111827;
            color: #cbd5e1;
            text-align: center;
            padding: 20px;
            margin-top: 30px;
        }


        /* ================= MOBILE ================= */

        @media(max-width: 750px) {

            .sensor-grid {
                grid-template-columns: 1fr;
            }

            .ml-grid {
                grid-template-columns: 1fr;
            }

            header h1 {
                font-size: 23px;
            }

        }

    </style>

</head>


<body>


<!-- ================= HEADER ================= -->

<header>

    <h1>
        Industrial Machine Health Monitoring
    </h1>

    <p>
        IoT-Based Real-Time Machine Monitoring & Predictive Analysis
    </p>

</header>



<div class="container">


    <!-- ================= MACHINE STATUS ================= -->

    <div class="status-card">

        <h2>
            Machine Status
        </h2>

        <div id="machineStatus"
             class="disconnected-status">

            WAITING FOR DATA

        </div>

        <p style="margin-top:15px; color:#64748b;">

            Last Updated:
            <span id="lastUpdate">
                --
            </span>

        </p>

    </div>



    <!-- ================= CONNECTION ================= -->

    <div class="connection">

        ESP32 Connection:

        <span id="connectionStatus"
              class="disconnected">

            WAITING FOR DATA

        </span>

    </div>



    <!-- ================= SENSOR VALUES ================= -->

    <div class="sensor-grid">


        <!-- IR SENSOR -->

        <div class="sensor-card">

            <div class="sensor-icon">
                ⚙️
            </div>

            <h3>
                Machine Motion
            </h3>

            <div class="sensor-value"
                 id="motion">

                --

            </div>

            <div class="sensor-unit">
                IR Sensor
            </div>

        </div>



        <!-- LDR -->

        <div class="sensor-card">

            <div class="sensor-icon">
                💡
            </div>

            <h3>
                Light Level
            </h3>

            <div class="sensor-value"
                 id="light">

                --

            </div>

            <div class="sensor-unit">
                %
            </div>

        </div>



        <!-- RAIN -->

        <div class="sensor-card">

            <div class="sensor-icon">
                💧
            </div>

            <h3>
                Water Detection
            </h3>

            <div class="sensor-value"
                 id="rain">

                --

            </div>

            <div class="sensor-unit">
                %
            </div>

        </div>


    </div>



    <!-- ================= ML ANALYSIS ================= -->

    <div class="ml-card">

        <h2>
            🤖 Machine Condition Analysis
        </h2>


        <div class="ml-grid">


            <div class="ml-box">

                <h3>
                    Machine Condition
                </h3>

                <p id="prediction">
                    --
                </p>

            </div>



            <div class="ml-box">

                <h3>
                    Abnormality Risk
                </h3>

                <p id="risk">
                    -- %
                </p>

            </div>



            <div class="ml-box">

                <h3>
                    Analysis Confidence
                </h3>

                <p id="confidence">
                    -- %
                </p>

            </div>


        </div>

    </div>



    <!-- ================= SENSOR ANALYSIS ================= -->

    <div class="analysis-card">

        <h2>
            📊 Live Sensor Analysis
        </h2>


        <!-- MACHINE MOTION -->

        <div class="parameter">

            <div class="parameter-title">

                <span>
                    Machine Motion
                </span>

                <span id="motionPercentage">
                    0%
                </span>

            </div>

            <div class="bar">

                <div id="motionBar"
                     class="bar-fill">
                </div>

            </div>

        </div>



        <!-- LIGHT -->

        <div class="parameter">

            <div class="parameter-title">

                <span>
                    Light Level
                </span>

                <span id="lightPercentage">
                    0%
                </span>

            </div>

            <div class="bar">

                <div id="lightBar"
                     class="bar-fill">
                </div>

            </div>

        </div>



        <!-- RAIN -->

        <div class="parameter">

            <div class="parameter-title">

                <span>
                    Water Detection
                </span>

                <span id="rainPercentage">
                    0%
                </span>

            </div>

            <div class="bar">

                <div id="rainBar"
                     class="bar-fill">
                </div>

            </div>

        </div>


    </div>



    <!-- ================= ALERT ================= -->

    <div id="alertBox">

        <h2 id="alertTitle">
            ⚠️ MACHINE ALERT
        </h2>

        <p id="alertMessage">
            Abnormal condition detected.
        </p>

    </div>


</div>



<!-- ================= FOOTER ================= -->

<footer>

    Smart Machine Health Monitoring System

    <br>

    Arduino UNO • ESP32 • IoT • Sensor Analytics

</footer>


<script>

async function updateDashboard() {
    try {
        const response = await fetch("/api/machine");
        const data = await response.json();

        document.getElementById("connectionStatus").innerText =
            data.connected ? "CONNECTED" : "DISCONNECTED";

        document.getElementById("machineStatus").innerText =
            data.connected ? (data.status || "HEALTHY") : "NO DATA";

        document.getElementById("motion").innerText =
            data.connected ? (data.motion ? "MOTION" : "NO MOTION") : "--";

        document.getElementById("light").innerText =
            data.connected ? (data.light || 0) : "--";

        document.getElementById("rain").innerText =
            data.connected ? (data.rain || 0) : "--";

        document.getElementById("prediction").innerText =
            data.prediction || "--";

        document.getElementById("risk").innerText =
            (data.risk || 0).toFixed(1) + " %";

        document.getElementById("confidence").innerText =
            (data.confidence || 0).toFixed(1) + " %";

        document.getElementById("lastUpdate").innerText =
            new Date().toLocaleTimeString();

    } catch (error) {
        document.getElementById("connectionStatus").innerText =
            "SERVER ERROR";
        console.log(error);
    }
}

updateDashboard();
setInterval(updateDashboard, 2000);

</script>

    try {


        // Get latest data from Flask

        const response =
            await fetch("/api/machine");


        const data =
            await response.json();



        // =================================================
        // CHECK CONNECTION
        // =================================================

        if (!data.connected) {


            document.getElementById(
                "connectionStatus"
            ).innerText =
                "DISCONNECTED";


            document.getElementById(
                "connectionStatus"
            ).className =
                "disconnected";


            document.getElementById(
                "machineStatus"
            ).innerText =
                "NO DATA";


            document.getElementById(
                "machineStatus"
            ).className =
                "disconnected-status";


            document.getElementById(
                "motion"
            ).innerText =
                "--";


            document.getElementById(
                "light"
            ).innerText =
                "--";


            document.getElementById(
                "rain"
            ).innerText =
                "--";


            document.getElementById(
                "prediction"
            ).innerText =
                "NO DATA";


            document.getElementById(
                "risk"
            ).innerText =
                "-- %";


            document.getElementById(
                "confidence"
            ).innerText =
                "-- %";


            document.getElementById(
                "alertBox"
            ).style.display =
                "none";


            return;

        }



        // =================================================
        // SENSOR VALUES
        // =================================================

        const motion =
            Number(data.motion);


        const light =
            Number(data.light);


        const rain =
            Number(data.rain);



        // =================================================
        // DISPLAY SENSOR VALUES
        // =================================================


        if (motion === 1) {

            document.getElementById(
                "motion"
            ).innerText =
                "MOTION";

        }
        else {

            document.getElementById(
                "motion"
            ).innerText =
                "NO MOTION";

        }


        document.getElementById(
            "light"
        ).innerText =
            light;


        document.getElementById(
            "rain"
        ).innerText =
            rain;



        // =================================================
        // MACHINE STATUS
        // =================================================

        const status =
            data.status || "HEALTHY";


        const statusElement =
            document.getElementById(
                "machineStatus"
            );


        statusElement.innerText =
            status;


        statusElement.className =
            "";


        if (status === "HEALTHY") {

            statusElement.classList.add(
                "healthy"
            );

        }

        else if (status === "WARNING") {

            statusElement.classList.add(
                "warning"
            );

        }

        else if (status === "CRITICAL") {

            statusElement.classList.add(
                "critical"
            );

        }



        // =================================================
        // ANALYSIS
        // =================================================

        const prediction =
            data.prediction || status;


        const risk =
            Number(data.risk || 0);


        const confidence =
            Number(data.confidence || 0);


        document.getElementById(
            "prediction"
        ).innerText =
            prediction;


        document.getElementById(
            "risk"
        ).innerText =
            risk.toFixed(1) + " %";


        document.getElementById(
            "confidence"
        ).innerText =
            confidence.toFixed(1) + " %";



        // =================================================
        // SENSOR BARS
        // =================================================

        // IR motion:
        // 0 = no motion
        // 1 = motion

        const motionPercent =
            motion === 1 ? 100 : 0;


        // LDR is already 0-100

        const lightPercent =
            Math.min(
                Math.max(light, 0),
                100
            );


        // Rain is already 0-100

        const rainPercent =
            Math.min(
                Math.max(rain, 0),
                100
            );



        document.getElementById(
            "motionBar"
        ).style.width =
            motionPercent + "%";


        document.getElementById(
            "lightBar"
        ).style.width =
            lightPercent + "%";


        document.getElementById(
            "rainBar"
        ).style.width =
            rainPercent + "%";



        document.getElementById(
            "motionPercentage"
        ).innerText =
            motionPercent + "%";


        document.getElementById(
            "lightPercentage"
        ).innerText =
            lightPercent.toFixed(0) + "%";


        document.getElementById(
            "rainPercentage"
        ).innerText =
            rainPercent.toFixed(0) + "%";



        // =================================================
        // CONNECTION STATUS
        // =================================================

        const connection =
            document.getElementById(
                "connectionStatus"
            );


        connection.innerText =
            "CONNECTED";


        connection.className =
            "connected";



        // =================================================
        // ALERT
        // =================================================

        const alertBox =
            document.getElementById(
                "alertBox"
            );


        const alertMessage =
            document.getElementById(
                "alertMessage"
            );


        const alertTitle =
            document.getElementById(
                "alertTitle"
            );



        if (status === "WARNING") {


            alertBox.style.display =
                "block";


            alertBox.className =
                "alert-warning";


            alertTitle.innerText =
                "⚠️ MACHINE WARNING";


            alertMessage.innerText =
                "Abnormal monitored condition detected. " +
                "Risk level: " +
                risk.toFixed(1) +
                "%";

        }


        else if (status === "CRITICAL") {


            alertBox.style.display =
                "block";


            alertBox.className =
                "alert-critical";


            alertTitle.innerText =
                "🚨 CRITICAL CONDITION";


            alertMessage.innerText =
                "High water/moisture or abnormal " +
                "machine condition detected. " +
                "Risk level: " +
                risk.toFixed(1) +
                "%";

        }


        else {


            alertBox.style.display =
                "none";

        }



        // =================================================
        // LAST UPDATE
        // =================================================

        const now =
            new Date();


        document.getElementById(
            "lastUpdate"
        ).innerText =
            now.toLocaleTimeString();


    }


    catch (error) {


        console.error(
            "Dashboard Error:",
            error
        );


        document.getElementById(
            "connectionStatus"
        ).innerText =
            "SERVER ERROR";


        document.getElementById(
            "connectionStatus"
        ).class

Dashboard 

![](DASHBOARD.png)

Authors

GNANESHH D.S

DARSHAN P.T

ARAVIND M

HEMAVARTHIINI V.S





