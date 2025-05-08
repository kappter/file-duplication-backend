# File Duplication Detector Backend

## Overview
This repository contains the Node.js/Express backend for the File Duplication Detector web application, deployed on Render’s free tier. It provides a `POST /upload` endpoint to process two file uploads, extract metadata (size, type, creation date, modified date, content hash), and return it to the frontend for duplication analysis. Files are deleted immediately after processing for privacy.

## File Structure
```
file-duplication-backend/
├── package.json
├── server.js
```

- **package.json**: Defines dependencies (`express`, `multer`) and the start script (`node server.js`).
- **server.js**: Implements the Express server with a `POST /upload` endpoint, using `multer` for file uploads and `fs.stat` for metadata extraction (including `birthtime` for creation date).

## Deployment (Web-Based, No Command Line)
1. **Add Files**:
   - Access https://github.com/kappter/file-duplication-backend.
   - Click **Add file** > **Create new file** or **Upload files**.
   - Upload `server.js` and `package.json` (copy from provided artifacts).
   - Commit to the `main` branch.
2. **Deploy on Render**:
   - Sign up at https://render.com with GitHub.
   - In the Dashboard, click **New** > **Web Service** > **Build and deploy from a Git repository**.
   - Connect `kappter/file-duplication-backend`.
   - Configure:
     - **Name**: `file-duplication-backend`
     - **Environment**: Node
     - **Branch**: `main`
     - **Build Command**: `npm install`
     - **Start Command**: `node server.js`
     - **Instance Type**: Free
   - Click **Create Web Service**.
   - Copy the URL (e.g., `https://file-duplication-backend.onrender.com`) after deployment.
3. **Update Frontend**:
   - In the frontend repository (`file-duplication-detector`), update `script.js`’s `BACKEND_URL` to the Render URL.
   - Commit via GitHub’s web interface.

## Testing
- Test the endpoint via the frontend (https://kappter.github.io/file-duplication-detector) by uploading files.
- Verify metadata includes creation date (`birthtime`), size, type, hash, and modified date.
- If issues arise, check Render’s **Logs** tab in the Dashboard.

## Limitations
- **Creation Date**: `birthtime` may be unavailable on some file systems (e.g., ext4); test with NTFS/APFS files.
- **Render Free Tier**: 750 hours/month, sleeps after 15 minutes of inactivity.
- **Privacy**: Files are deleted immediately; verify Render’s FERPA compliance.

## License
For educational use. Not for commercial purposes.