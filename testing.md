<Plan>
1. Save image testing playbook to /app/image_testing.md
2. Install expo-image-picker for image uploads
3. Add EMERGENT_LLM_KEY to backend/.env
4. Rewrite backend server.py with:
   - Chat sessions + messages MongoDB models
   - POST /api/chat/session (create new session)
   - GET /api/chat/sessions (list sessions)
   - GET /api/chat/session/{id}/messages (get messages)
   - DELETE /api/chat/session/{id}
   - POST /api/chat/send (send message with optional base64 image, uses GPT-5.2)
   - System prompt makes AI identify as "Cuffli AI dibuat oleh cuffli"
5. Rewrite frontend:
   - Root layout with GestureHandlerRootView
   - Custom drawer + chat screen (single index.tsx orchestrator, plus components)
   - Dark theme #000, sage green accents
   - Image attachment support
6. Test with testing agent
</Plan>
Action: file_editor create /app/image_testing.md --file-text "## TEST AGENT PROMPT – IMAGE INTEGRATION RULES ##
You are the Test Agent responsible for validating image integrations.
Follow these rules exactly. Do not overcomplicate.

*** Image Handling Rules ***
- Always use base64-encoded images for all tests and requests.
- Accepted formats: JPEG, PNG, WEBP only.
- Do not use SVG, BMP, HEIC, or other formats.
- Do not upload blank, solid-color, or uniform-variance images.
- Every image must contain real visual features — such as objects, edges, textures, or shadows.
- If the image is not PNG/JPEG/WEBP, transcode it to PNG or JPEG before upload.
  ## Fix Example:
    If you read a .jpg but the content is actually PNG after conversion or compression — this is invalid.
    Always re-detect and update the MIME after transformations.
- If the image is animated (e.g., GIF, APNG, WEBP animation), extract the first frame only.
- Resize large images to reasonable bounds (avoid oversized payloads).
"
Observation: Create successful: /app/image_testing.md