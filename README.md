<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced SEO & Social Meta Tag Generator</title>
    <style>
        :root {
            --primary: #4F46E5;
            --primary-hover: #4338CA;
            --bg: #F3F4F6;
            --card-bg: #FFFFFF;
            --text-main: #1F2937;
            --text-muted: #6B7280;
            --border: #D1D5DB;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg);
            color: var(--text-main);
            margin: 0;
            padding: 30px 15px;
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
        }

        .header h1 {
            margin: 0;
            color: var(--primary);
        }

        .header p {
            color: var(--text-muted);
            margin-top: 5px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr;
            gap: 25px;
        }

        @media (min-width: 900px) {
            .container {
                grid-template-columns: 1fr 1fr;
            }
        }

        .card {
            background: var(--card-bg);
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
        }

        .section-title {
            font-size: 1.2rem;
            margin-top: 0;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--bg);
        }

        .form-group {
            margin-bottom: 18px;
        }

        .label-wrapper {
            display: flex;
            justify-content: space-between;
            margin-bottom: 6px;
        }

        label {
            font-weight: 600;
            font-size: 0.9rem;
        }

        .char-count {
            font-size: 0.8rem;
            color: var(--text-muted);
        }
        
        .char-count.warning { color: #D97706; }
        .char-count.error { color: #DC2626; }

        input[type="text"], input[type="url"], textarea, select {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid var(--border);
            border-radius: 6px;
            font-family: inherit;
            font-size: 0.95rem;
            box-sizing: border-box;
            transition: border-color 0.2s;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
        }

        textarea { resize: vertical; height: 80px; }

        /* Google Preview Styles */
        .google-preview {
            background: #fff;
            padding: 15px;
            border-radius: 8px;
            border: 1px solid var(--border);
            margin-bottom: 25px;
            font-family: Arial, sans-serif;
        }

        .g-url {
            color: #202124;
            font-size: 14px;
            margin-bottom: 2px;
            display: block;
        }

        .g-title {
            color: #1a0dab;
            font-size: 20px;
            line-height: 1.3;
            margin: 0 0 3px 0;
            font-weight: 400;
            cursor: pointer;
            text-decoration: none;
        }
        
        .g-title:hover { text-decoration: underline; }

        .g-desc {
            color: #4d5156;
            font-size: 14px;
            line-height: 1.58;
            margin: 0;
            word-wrap: break-word;
        }

        /* Output Area */
        #outputCode {
            width: 100%;
            height: 350px;
            background-color: #1E1E1E;
            color: #D4D4D4;
            font-family: 'Consolas', 'Courier New', monospace;
            padding: 15px;
            border: none;
            border-radius: 6px;
            box-sizing: border-box;
            resize: none;
            margin-bottom: 15px;
        }

        button {
            width: 100%;
            padding: 12px;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.3s;
        }

        button:hover { background-color: var(--primary-hover); }
        
        button.copy-btn { background-color: #10B981; }
        button.copy-btn:hover { background-color: #059669; }

    </style>
</head>
<body>

<div class="header">
    <h1>Advanced SEO Meta Generator</h1>
    <p>Create perfect tags for Search Engines, Facebook, and Twitter.</p>
</div>

<div class="container">
    <div class="card">
        <h2 class="section-title">⚙️ Basic & Social Details</h2>
        
        <div class="form-group">
            <div class="label-wrapper">
                <label>Site Title</label>
                <span class="char-count" id="titleCount">0 / 60</span>
            </div>
            <input type="text" id="siteTitle" placeholder="e.g., Best Micro-SaaS Tools 2026">
        </div>

        <div class="form-group">
            <div class="label-wrapper">
                <label>Site Description</label>
                <span class="char-count" id="descCount">0 / 160</span>
            </div>
            <textarea id="siteDesc" placeholder="Brief, catchy description for search results..."></textarea>
        </div>

        <div class="form-group">
            <label>Canonical URL</label>
            <input type="url" id="siteUrl" placeholder="https://www.yourwebsite.com">
        </div>

        <div class="form-group">
            <label>Featured Image URL (For Social Sharing)</label>
            <input type="url" id="siteImage" placeholder="https://www.yourwebsite.com/image.jpg">
        </div>

        <div class="form-group">
            <label>Keywords (Comma separated)</label>
            <input type="text" id="siteKeywords" placeholder="SaaS, generator tool, free utility">
        </div>

        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
            <div class="form-group">
                <label>Robots Indexing</label>
                <select id="robotIndex">
                    <option value="index, follow">Index & Follow</option>
                    <option value="noindex, nofollow">No Index & No Follow</option>
                    <option value="index, nofollow">Index & No Follow</option>
                </select>
            </div>
            <div class="form-group">
                <label>Language Locale</label>
                <input type="text" id="siteLocale" value="en_US" placeholder="e.g., en_US or hi_IN">
            </div>
        </div>

        <div class="form-group">
            <label>Author / Twitter Handle</label>
            <input type="text" id="siteAuthor" placeholder="@yourhandle or Your Name">
        </div>
    </div>

    <div class="card">
        <h2 class="section-title">👁️ Live Search Preview</h2>
        <div class="google-preview">
            <span class="g-url" id="previewUrl">www.yourwebsite.com</span>
            <h3 class="g-title" id="previewTitle">Your Site Title Will Appear Here</h3>
            <p class="g-desc" id="previewDesc">Your website description will show up right here. Make sure it is descriptive and includes relevant keywords to attract users from search engines.</p>
        </div>

        <h2 class="section-title">💻 Generated Code</h2>
        <textarea id="outputCode" readonly placeholder="Start typing to generate your meta tags automatically..."></textarea>
        <button class="copy-btn" id="copyBtn" onclick="copyCode()">Copy Code to Clipboard</button>
    </div>
</div>

<script>
    // Elements
    const inputs = ['siteTitle', 'siteDesc', 'siteUrl', 'siteImage', 'siteKeywords', 'robotIndex', 'siteLocale', 'siteAuthor'];
    
    // Add event listeners for real-time generation
    inputs.forEach(id => {
        document.getElementById(id).addEventListener('input', updateAll);
    });

    function updateAll() {
        updateCounters();
        updatePreview();
        generateTags();
    }

    function updateCounters() {
        const titleLen = document.getElementById('siteTitle').value.length;
        const descLen = document.getElementById('siteDesc').value.length;
        
        const titleCount = document.getElementById('titleCount');
        const descCount = document.getElementById('descCount');

        titleCount.innerText = `${titleLen} / 60`;
        descCount.innerText = `${descLen} / 160`;

        // Title Warning Colors
        titleCount.className = 'char-count ' + (titleLen > 60 ? 'error' : (titleLen > 50 ? 'warning' : ''));
        // Desc Warning Colors
        descCount.className = 'char-count ' + (descLen > 160 ? 'error' : (descLen > 150 ? 'warning' : ''));
    }

    function updatePreview() {
        const title = document.getElementById('siteTitle').value || 'Your Site Title Will Appear Here';
        const desc = document.getElementById('siteDesc').value || 'Your website description will show up right here. Make sure it is descriptive and includes relevant keywords to attract users from search engines.';
        const url = document.getElementById('siteUrl').value || 'www.yourwebsite.com';

        // Clean URL for preview
        const cleanUrl = url.replace(/^https?:\/\//,'').replace(/\/$/,'');

        document.getElementById('previewTitle').innerText = title;
        document.getElementById('previewDesc').innerText = desc.length > 160 ? desc.substring(0, 157) + '...' : desc;
        document.getElementById('previewUrl').innerText = cleanUrl;
    }

    function generateTags() {
        const title = document.getElementById('siteTitle').value.trim();
        const desc = document.getElementById('siteDesc').value.trim();
        const url = document.getElementById('siteUrl').value.trim();
        const image = document.getElementById('siteImage').value.trim();
        const keywords = document.getElementById('siteKeywords').value.trim();
        const robots = document.getElementById('robotIndex').value;
        const locale = document.getElementById('siteLocale').value.trim();
        const author = document.getElementById('siteAuthor').value.trim();

        let meta = '\n';
        meta += `<meta charset="UTF-8">\n`;
        meta += `<meta name="viewport" content="width=device-width, initial-scale=1.0">\n`;
        if(title) {
            meta += `<title>${title}</title>\n`;
            meta += `<meta name="title" content="${title}">\n`;
        }
        if(desc) meta += `<meta name="description" content="${desc}">\n`;
        if(keywords) meta += `<meta name="keywords" content="${keywords}">\n`;
        if(author) meta += `<meta name="author" content="${author}">\n`;
        if(url) meta += `<link rel="canonical" href="${url}">\n`;
        meta += `<meta name="robots" content="${robots}">\n\n`;

        meta += '\n';
        meta += `<meta property="og:type" content="website">\n`;
        if(url) meta += `<meta property="og:url" content="${url}">\n`;
        if(title) meta += `<meta property="og:title" content="${title}">\n`;
        if(desc) meta += `<meta property="og:description" content="${desc}">\n`;
        if(image) meta += `<meta property="og:image" content="${image}">\n`;
        if(locale) meta += `<meta property="og:locale" content="${locale}">\n\n`;

        meta += '\n';
        meta += `<meta property="twitter:card" content="summary_large_image">\n`;
        if(url) meta += `<meta property="twitter:url" content="${url}">\n`;
        if(title) meta += `<meta property="twitter:title" content="${title}">\n`;
        if(desc) meta += `<meta property="twitter:description" content="${desc}">\n`;
        if(image) meta += `<meta property="twitter:image" content="${image}">\n`;
        if(author && author.startsWith('@')) meta += `<meta name="twitter:creator" content="${author}">\n`;

        document.getElementById('outputCode').value = meta;
    }

    function copyCode() {
        const outputElement = document.getElementById('outputCode');
        if(!outputElement.value) return;
        
        outputElement.select();
        outputElement.setSelectionRange(0, 99999);
        
        navigator.clipboard.writeText(outputElement.value).then(() => {
            const copyBtn = document.getElementById('copyBtn');
            copyBtn.innerText = "✅ Code Copied!";
            copyBtn.style.backgroundColor = "#059669"; // Darker green
            
            setTimeout(() => {
                copyBtn.innerText = "Copy Code to Clipboard";
                copyBtn.style.backgroundColor = "#10B981"; // Original green
            }, 2500);
        });
    }

    // Initialize with empty state
    updateAll();
</script>

</body>
</html>
