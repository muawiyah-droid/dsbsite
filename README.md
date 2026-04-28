<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DSB - Doha Street Board</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Inter', sans-serif; background: #0a0a0f; color: #fff; min-height: 100vh; }
        
        .landing {
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            min-height: 100vh; padding: 40px 20px; text-align: center;
            background: linear-gradient(135deg, #0a0a0f 0%, #1a1a2e 50%, #16213e 100%);
        }
        .landing .logo { font-size: 14px; font-weight: 700; letter-spacing: 3px; color: #00d4aa; margin-bottom: 40px; }
        .landing .offer-badge {
            background: #00d4aa; color: #0a0a0f; padding: 8px 20px; border-radius: 50px;
            font-size: 12px; font-weight: 700; letter-spacing: 1px; margin-bottom: 30px;
        }
        .landing h1 { font-size: 36px; font-weight: 800; line-height: 1.1; margin-bottom: 15px; }
        .landing h1 span { color: #00d4aa; }
        .landing p.sub { font-size: 16px; color: #8892b0; margin-bottom: 40px; max-width: 400px; }
        .landing .scan-info {
            background: rgba(255,255,255,0.05); border: 1px solid rgba(0,212,170,0.2);
            border-radius: 16px; padding: 20px 30px; margin-bottom: 30px;
        }
        .landing .scan-info .label { font-size: 11px; color: #8892b0; text-transform: uppercase; letter-spacing: 2px; }
        .landing .scan-info .value { font-size: 28px; font-weight: 800; color: #00d4aa; margin-top: 5px; }
        .landing .scan-info .detail { font-size: 13px; color: #8892b0; margin-top: 8px; }
        .landing .cta-btn {
            background: #00d4aa; color: #0a0a0f; border: none; padding: 16px 40px;
            border-radius: 12px; font-size: 16px; font-weight: 700; cursor: pointer;
            transition: all 0.3s; text-decoration: none; display: inline-block;
        }
        .landing .cta-btn:hover { transform: translateY(-2px); box-shadow: 0 10px 30px rgba(0,212,170,0.3); }
        .landing .powered { margin-top: 40px; font-size: 11px; color: #555; letter-spacing: 2px; }
        .landing .powered span { color: #00d4aa; font-weight: 700; }
        
        .admin { display: none; padding: 40px; max-width: 1200px; margin: 0 auto; }
        .admin-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 40px; }
        .admin-header h1 { font-size: 24px; font-weight: 800; }
        .admin-header h1 span { color: #00d4aa; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; margin-bottom: 40px; }
        .stat-card {
            background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06);
            border-radius: 16px; padding: 24px;
        }
        .stat-card .label { font-size: 12px; color: #8892b0; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 8px; }
        .stat-card .value { font-size: 32px; font-weight: 800; color: #fff; }
        .stat-card .change { font-size: 13px; margin-top: 5px; }
        .stat-card .change.up { color: #00d4aa; }
        .stat-card .change.down { color: #ff6b6b; }
        
        .table-container {
            background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06);
            border-radius: 16px; overflow: hidden;
        }
        .table-container table { width: 100%; border-collapse: collapse; }
        .table-container th {
            background: rgba(0,212,170,0.1); padding: 16px 20px; text-align: left;
            font-size: 11px; text-transform: uppercase; letter-spacing: 1px; color: #00d4aa;
            font-weight: 600;
        }
        .table-container td { padding: 16px 20px; border-bottom: 1px solid rgba(255,255,255,0.04); font-size: 14px; }
        .table-container tr:hover { background: rgba(255,255,255,0.02); }
        .table-container .badge {
            display: inline-block; padding: 4px 12px; border-radius: 20px;
            font-size: 11px; font-weight: 600;
        }
        .badge.westbay { background: rgba(0,212,170,0.15); color: #00d4aa; }
        .badge.lusail { background: rgba(100,149,237,0.15); color: #6495ed; }
        .badge.thepearl { background: rgba(255,215,0,0.15); color: #ffd700; }
        .badge.doha { background: rgba(255,105,180,0.15); color: #ff69b4; }
        
        .toggle-btn {
            background: rgba(0,212,170,0.1); color: #00d4aa; border: 1px solid rgba(0,212,170,0.3);
            padding: 10px 24px; border-radius: 8px; font-size: 13px; font-weight: 600;
            cursor: pointer; transition: all 0.3s;
        }
        .toggle-btn:hover { background: rgba(0,212,170,0.2); }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        .live-dot {
            display: inline-block; width: 8px; height: 8px; background: #00d4aa;
            border-radius: 50%; margin-right: 8px; animation: pulse 2s infinite;
        }
    </style>
</head>
<body>

<div class="landing" id="landingPage">
    <div class="logo">DSB</div>
    <div class="offer-badge">EXCLUSIVE OFFER</div>
    <h1>Get <span>20% Off</span><br>Your Next Order</h1>
    <p class="sub">Scanned from a DSB-enabled delivery bike in Doha. Limited time only.</p>
    
    <div class="scan-info">
        <div class="label">Scan Number</div>
        <div class="value" id="scanCount">Loading...</div>
        <div class="detail" id="scanDetail">Tracking your engagement...</div>
    </div>
    
    <a href="#" class="cta-btn" onclick="claimOffer(); return false;">Claim Offer</a>
    
    <div class="powered">POWERED BY <span>DSB</span> — DOHA STREET BOARD</div>
</div>

<div class="admin" id="adminPage">
    <div class="admin-header">
        <h1><span>DSB</span> Dashboard</h1>
        <button class="toggle-btn" onclick="showLanding()">&larr; Back to Landing</button>
    </div>
    
    <div class="stats-grid">
        <div class="stat-card">
            <div class="label">Total Scans</div>
            <div class="value" id="totalScans">0</div>
            <div class="change up">&uarr; Live tracking active</div>
        </div>
        <div class="stat-card">
            <div class="label">Today's Scans</div>
            <div class="value" id="todayScans">0</div>
            <div class="change up">&uarr; Real-time</div>
        </div>
        <div class="stat-card">
            <div class="label">Active Bikes</div>
            <div class="value">3</div>
            <div class="change up">&uarr; Pilot fleet</div>
        </div>
        <div class="stat-card">
            <div class="label">Top Location</div>
            <div class="value" style="font-size:20px;">West Bay</div>
            <div class="change up">42% of scans</div>
        </div>
    </div>
    
    <div class="table-container">
        <table>
            <thead>
                <tr>
                    <th><span class="live-dot"></span>Time</th>
                    <th>Location</th>
                    <th>Bike ID</th>
                    <th>Device</th>
                    <th>Status</th>
                </tr>
            </thead>
            <tbody id="scanTable">
            </tbody>
        </table>
    </div>
</div>

<script>
function getScans() {
    const stored = localStorage.getItem('dsb_scans');
    return stored ? JSON.parse(stored) : [];
}

function saveScan(scan) {
    const scans = getScans();
    scans.unshift(scan);
    localStorage.setItem('dsb_scans', JSON.stringify(scans));
    return scans;
}

function seedMockData() {
    if (getScans().length > 0) return;
    const locations = ['West Bay', 'Lusail', 'The Pearl', 'Doha', 'West Bay', 'Lusail'];
    const bikes = ['DSB-001', 'DSB-002', 'DSB-003', 'DSB-001', 'DSB-002', 'DSB-003'];
    const now = new Date();
    
    for (let i = 0; i < 6; i++) {
        const time = new Date(now.getTime() - i * 45 * 60000);
        saveScan({
            id: 127 - i,
            timestamp: time.toISOString(),
            location: locations[i],
            bikeId: bikes[i],
            device: 'Mobile',
            status: 'Converted'
        });
    }
}

function initLanding() {
    seedMockData();
    let location = 'Doha';
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
            (pos) => {
                const lat = pos.coords.latitude;
                if (lat > 25.35) location = 'Lusail';
                else if (lat > 25.30) location = 'The Pearl';
                else location = 'West Bay';
                recordScan(location);
            },
            () => recordScan('Doha')
        );
    } else {
        recordScan('Doha');
    }
}

function recordScan(location) {
    const scans = getScans();
    const newScan = {
        id: scans.length > 0 ? Math.max(...scans.map(s => s.id)) + 1 : 127,
        timestamp: new Date().toISOString(),
        location: location,
        bikeId: 'DSB-001',
        device: navigator.userAgent.includes('Mobile') ? 'Mobile' : 'Desktop',
        status: 'Active'
    };
    saveScan(newScan);
    document.getElementById('scanCount').textContent = '#' + newScan.id;
    document.getElementById('scanDetail').textContent = 
        'Scanned from ' + location + ' at ' + formatTime(newScan.timestamp);
}

function claimOffer() {
    alert('Offer claimed! In production, this redirects to partner restaurant.');
}

function initAdmin() {
    seedMockData();
    const scans = getScans();
    document.getElementById('totalScans').textContent = scans.length;
    const today = new Date().toDateString();
    const todayScans = scans.filter(s => new Date(s.timestamp).toDateString() === today);
    document.getElementById('todayScans').textContent = todayScans.length;
    
    const tbody = document.getElementById('scanTable');
    tbody.innerHTML = scans.slice(0, 20).map(scan => {
        const locClass = scan.location.toLowerCase().replace(/\\s/g, '');
        return '<tr>' +
            '<td>' + formatTime(scan.timestamp) + '</td>' +
            '<td><span class="badge ' + locClass + '">' + scan.location + '</span></td>' +
            '<td>' + scan.bikeId + '</td>' +
            '<td>' + scan.device + '</td>' +
            '<td><span style="color:#00d4aa;font-weight:600;">' + scan.status + '</span></td>' +
        '</tr>';
    }).join('');
}

function formatTime(iso) {
    const d = new Date(iso);
    return d.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit', hour12: true });
}

function showLanding() {
    document.getElementById('adminPage').style.display = 'none';
    document.getElementById('landingPage').style.display = 'flex';
}

function showAdmin() {
    document.getElementById('landingPage').style.display = 'none';
    document.getElementById('adminPage').style.display = 'block';
    initAdmin();
}

const urlParams = new URLSearchParams(window.location.search);
if (urlParams.get('admin') === 'dsb2026') {
    showAdmin();
} else {
    initLanding();
}
</script>

</body>
</html>
