# AssaultCube Silent Aim & Magic Bullet

This is a method to implement **Silent Aim** and **Magic Bullet** by modifying the bullet trajectory to always hit the closest target’s head.

## 🛠️ How It Works
This exploit hooks into the game's shooting function and overrides the bullet’s position, redirecting it to the nearest enemy’s **head position**.

### 🔧 Code Example:
```cpp
typedef bool(__thiscall* tShoot)(DWORD*, Vector3*);
tShoot oShoot = nullptr;

bool __fastcall hkShoot(DWORD* _this, void* edx, Vector3* Bullet)
{
    auto Target = GetCloestEntity();
    if (Target)
    {
        *Bullet = Target->HeadPosition;
    }

    return oShoot(_this, Bullet);
}

void Hooks()
{
    void* pShoot = reinterpret_cast<void*>(0x463600); // Function address

    MH_CreateHook(pShoot, &hkShoot, reinterpret_cast<LPVOID*>(&oShoot));
    MH_EnableHook(pShoot);
}
```

## ⚠️ Disclaimer
You must add the hook when in a empty match to avoid crash :(

// This project is for educational purposes only.
