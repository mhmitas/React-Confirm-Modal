# React-Confirm-Modal

confirm.js
```js
import React from 'react';
import { createRoot } from 'react-dom/client';
import ConfirmModal from './ConfirmModal';

const confirm = (message) => {
    return new Promise((resolve, reject) => {
        const div = document.createElement('div');
        document.body.appendChild(div);

        const root = createRoot(div);

        const handleConfirm = () => {
            cleanup();
            resolve(true);
        };

        const handleCancel = () => {
            cleanup();
            resolve(false);
        };

        const cleanup = () => {
            root.unmount();
            div.remove();
        };

        root.render(
            <ConfirmModal
                message={message}
                onConfirm={handleConfirm}
                onCancel={handleCancel}
            />
        );
    });
};

export default confirm;
```

ConfirmModal.js
```js
import React from 'react';

const ConfirmModal = ({ message, onConfirm, onCancel }) => {
    const handleOverlayClick = (e) => {
        if (e.target === e.currentTarget) {
            onCancel();
        }
    };

    return (
        <div
            className="fixed inset-0 flex items-center justify-center bg-gray-800 bg-opacity-75 z-50"
            onClick={handleOverlayClick}
        >
            <div className="bg-white text-slate-950 rounded-lg shadow-lg p-6 w-96">
                <h2 className="text-lg font-semibold mb-4">Confirm Action</h2>
                <p className="mb-6">{message}</p>
                <div className="flex justify-end space-x-4">
                    <button className="btn btn-secondary" onClick={onCancel}>
                        Cancel
                    </button>
                    <button className="btn btn-primary" onClick={onConfirm}>
                        Confirm
                    </button>
                </div>
            </div>
        </div>
    );
};

export default ConfirmModal;
```
