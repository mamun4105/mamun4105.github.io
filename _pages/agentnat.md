---
layout: default
title: "AgentNat - InVEST Assistant"
permalink: /agentnat/
---

<style>
    .page__content {
        padding: 0 !important;
        margin: 0 !important;
        max-width: 100% !important;
    }
    .page {
        width: 100% !important;
    }
    .agentnat-container {
        width: 100%;
        height: calc(100vh - 100px);
        margin: 0;
        padding: 0;
        position: relative;
        overflow: hidden;
    }
    .agentnat-container iframe {
        width: 100%;
        height: 100%;
        border: none;
        display: block;
    }
    .browser-warning {
        display: none;
        text-align: center;
        padding: 60px 20px;
        background: #f8f9fa;
    }
    .browser-warning.show {
        display: block;
    }
    .browser-warning h2 {
        color: #333;
        margin-bottom: 20px;
    }
    .browser-warning p {
        font-size: 1.1em;
        color: #666;
        margin-bottom: 30px;
    }
    .open-button {
        display: inline-block;
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        color: white;
        padding: 15px 40px;
        border-radius: 30px;
        text-decoration: none;
        font-weight: bold;
        font-size: 1.2em;
        box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
    }
    .open-button:hover {
        color: white;
        text-decoration: none;
        box-shadow: 0 8px 20px rgba(102, 126, 234, 0.6);
    }
</style>

<div class="agentnat-container" id="iframeContainer">
    <iframe 
        id="agentnatFrame"
        src="https://mamun4105-natrag.hf.space?embed=true" 
        frameborder="0"
        title="AgentNat - InVEST Assistant"
        allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
        sandbox="allow-forms allow-modals allow-popups allow-popups-to-escape-sandbox allow-same-origin allow-scripts allow-downloads"
        allowfullscreen
    ></iframe>
</div>

<div class="browser-warning" id="browserWarning">
    <h2>🌐 Browser Compatibility Notice</h2>
    <p>
        Your browser's security settings are preventing the embedded view from loading.<br>
        Please click the button below to open AgentNat in a new tab.
    </p>
    <a href="https://mamun4105-natrag.hf.space" target="_blank" class="open-button">
        🚀 Open AgentNat
    </a>
    <p style="margin-top: 30px; font-size: 0.9em; color: #999;">
        <strong>Tip for Edge/Safari users:</strong> You can enable third-party cookies in your browser settings to use the embedded view.
    </p>
</div>

<script>
    // Detect if iframe fails to load (especially in Edge/Safari)
    var iframe = document.getElementById('agentnatFrame');
    var warning = document.getElementById('browserWarning');
    var container = document.getElementById('iframeContainer');
    var loaded = false;
    
    // Listen for iframe load
    iframe.addEventListener('load', function() {
        loaded = true;
    });
    
    // Check after 3 seconds if iframe loaded
    setTimeout(function() {
        // Try to detect if iframe is blocked by checking if we can access it
        try {
            var iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
            // If we get here without error, iframe may be loading
        } catch(e) {
            // Cross-origin is expected and means it's loading
            if (e.name === 'SecurityError') {
                loaded = true;
            }
        }
        
        // Show warning if still not loaded
        if (!loaded) {
            container.style.display = 'none';
            warning.classList.add('show');
        }
    }, 3000);
    
    // Also detect blank iframe after load
    iframe.addEventListener('load', function() {
        setTimeout(function() {
            try {
                if (iframe.contentWindow.location.href === 'about:blank') {
                    container.style.display = 'none';
                    warning.classList.add('show');
                }
            } catch(e) {
                // Cross-origin means it loaded successfully
            }
        }, 500);
    });
</script>
