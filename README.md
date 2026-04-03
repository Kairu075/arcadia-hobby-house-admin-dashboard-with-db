@extends('layouts.profile')
@section('main')

<style>
  /* ── SIDEBAR ── */
  .sidebar {
    background: #1e2d5a;
    border-radius: 14px;
    overflow: hidden;
  }
  .sidebar-link {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 18px;
    font-size: 14px;
    font-weight: 600;
    color: rgba(255,255,255,0.65);
    transition: 0.2s;
    text-decoration: none;
    border-radius: 10px;
    margin: 2px 10px;
    cursor: pointer;
  }
  .sidebar-link:hover {
    background: rgba(255,255,255,0.08);
    color: #fff;
  }
  .sidebar-link.active {
    background: #2550d4;
    color: #fff;
  }
  .sidebar-link.logout:hover {
    color: #fca5a5;
    background: rgba(239,68,68,0.15);
  }
  @media (max-width: 768px) {
    .sidebar { border-radius: 5px; }
  }

  /* ── Orders ── */
  .order-card {
    background: #fff;
    border: 1px solid #DBEAFE;
    border-radius: 1rem;
    padding: 1rem 1.25rem;
    transition: box-shadow .18s;
  }
  .order-card:hover { box-shadow: 0 4px 16px rgba(59,130,246,.1); }
  .order-id    { font-weight: 700; color: #1E3A5F; font-size: .9rem; }
  .order-date  { color: #94a3b8; font-size: .78rem; margin-top: .15rem; }
  .order-price { font-weight: 700; color: #3B82F6; font-size: 1.05rem; }

  /* ── Wishlist ── */
  .wish-card {
    background: #fff;
    border: 1px solid #DBEAFE;
    border-radius: 1rem;
    padding: 1rem;
    height: 100%;
    transition: box-shadow .18s;
  }
  .wish-card:hover { box-shadow: 0 4px 16px rgba(59,130,246,.1); }
  .wish-name  { font-weight: 700; color: #1E3A5F; font-size: .88rem; margin-bottom: .35rem; }
  .wish-price { font-weight: 700; color: #3B82F6; font-size: .95rem; margin-bottom: .75rem; }
  .wish-btn {
    width: 100%;
    background: #3B82F6;
    color: #fff;
    border: none;
    border-radius: .6rem;
    padding: .45rem;
    font-size: .82rem;
    font-weight: 600;
    cursor: pointer;
    transition: background .18s;
  }
  .wish-btn:hover { background: #2563EB; }

  /* ── Settings ── */
  .content-card {
    background: #fff;
    border: 1px solid #DBEAFE;
    border-radius: 1rem;
    padding: 1.25rem;
  }
  .content-card-title {
    color: #1E3A5F;
    font-size: .9rem;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: .4rem;
  }
  .edit-btn {
    background: none;
    border: none;
    color: #3B82F6;
    font-size: .78rem;
    display: flex;
    align-items: center;
    gap: .25rem;
    cursor: pointer;
    padding: 0;
  }
  .edit-btn:hover { color: #2563EB; }
  .info-tile {
    background: #EFF6FF;
    border-radius: .75rem;
    padding: .75rem;
  }
  .info-tile .label {
    color: #6B8DB5;
    font-size: .72rem;
    margin-bottom: .15rem;
  }
  .info-tile .value {
    color: #1E3A5F;
    font-size: .875rem;
    font-weight: 600;
    word-break: break-all;
  }
  .sec-btn {
    width: 100%;
    text-align: left;
    border-radius: .75rem;
    padding: .75rem 1rem;
    font-size: .875rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid #DBEAFE;
    background: #EFF6FF;
    color: #334155;
    transition: background .18s;
    cursor: pointer;
  }
  .sec-btn:hover { background: #DBEAFE; }
  .sec-btn.danger {
    background: #fff1f2;
    border-color: #fecdd3;
    color: #f87171;
  }
  .sec-btn.danger:hover { background: #fee2e2; }

  /* ── Shared ── */
  .empty-state { text-align: center; padding: 3rem 1rem; color: #94a3b8; }
  .empty-state i { font-size: 2.5rem; display: block; margin-bottom: .75rem; }
  .section-title { color: #1E3A5F; font-weight: 700; font-size: 1.1rem; margin-bottom: 1rem; }
</style>

<div class="row g-4 align-items-start">

  {{-- ═══════════════════════════════
       SIDEBAR
  ═══════════════════════════════ --}}
  <aside class="sidebar col-12 col-md-4 col-lg-3 mb-4 w-100">

    {{-- Profile --}}
    <div class="text-center p-4 border-bottom border-light border-opacity-10">
      <div class="mx-auto mb-2 d-flex align-items-center justify-content-center"
           style="width:64px;height:64px;border-radius:50%;background:#4e85f4;
                  color:#fff;font-size:24px;font-weight:800;
                  box-shadow:0 0 0 4px rgba(78,133,244,0.28);">
        {{ strtoupper(substr($user->first_name, 0, 1)) }}
      </div>
      <p class="text-white fw-bold mb-0">
        {{ $user->first_name }} {{ $user->last_name }}
      </p>
      <p class="text-white-50 small mb-2">
        {{ $user->email }}
      </p>
      <span class="badge bg-light text-dark px-3 py-2">
        ⭐ Hobby Enthusiast
      </span>
    </div>

    {{-- Nav --}}
    <nav class="py-3" role="tablist">
      <a class="sidebar-link active"
         data-bs-toggle="tab"
         href="#orders"
         role="tab">
        <i class="fa-solid fa-box-open"></i>
        My Orders
      </a>
      <a class="sidebar-link"
         data-bs-toggle="tab"
         href="#wishlist"
         role="tab">
        <i class="fa-regular fa-heart"></i>
        Wishlist
      </a>
      <a class="sidebar-link"
         data-bs-toggle="tab"
         href="#settings"
         role="tab">
        <i class="fa-solid fa-gear"></i>
        Settings
      </a>
      <div class="mx-3 my-1" style="border-top:1px solid rgba(255,255,255,0.1);"></div>
      <form action="{{ route('logout') }}" method="POST">
        @csrf
        <button type="submit"
                class="sidebar-link logout w-100 border-0 bg-transparent text-start">
          <i class="fa-solid fa-right-from-bracket"></i>
          Logout
        </button>
      </form>
    </nav>

  </aside>

  {{-- ═══════════════════════════════
       TAB CONTENT
  ═══════════════════════════════ --}}
  <div class="col-12 col-md-8 col-lg-9">
    <div class="tab-content" id="accountTabContent">

      {{-- ================= ORDERS ================= --}}
      <div class="tab-pane fade show active" id="orders" role="tabpanel">

        <h1 class="section-title">
          <i class="fa-solid fa-box-open me-2 text-primary"></i>My Orders
        </h1>

        @if(isset($orders) && count($orders) > 0)
          <div class="d-flex flex-column gap-3">
            @foreach($orders as $item)
              <div class="order-card">
                <div class="d-flex justify-content-between align-items-center">
                  <div>
                    <div class="order-id">
                      ORD-{{ str_pad($item->id, 3, '0', STR_PAD_LEFT) }}
                    </div>
                    <div class="order-date">
                      <i class="fa-regular fa-calendar me-1"></i>
                      {{ \Carbon\Carbon::parse($item->created_at)->format('M d, Y') }}
                    </div>
                  </div>
                  <div class="text-end">
                    <div class="order-price">₱{{ number_format($item->price, 2) }}</div>
                    @if(isset($item->status))
                      @php
                        $statusClass = match($item->status) {
                          'Delivered'  => 'text-bg-success',
                          'Shipped'    => 'text-bg-info',
                          'Processing' => 'text-bg-primary',
                          'Pending'    => 'text-bg-warning',
                          'Cancelled'  => 'text-bg-danger',
                          default      => 'text-bg-secondary',
                        };
                      @endphp
                      <span class="badge rounded-pill {{ $statusClass }} mt-1"
                            style="font-size:.72rem;">
                        {{ $item->status }}
                      </span>
                    @endif
                  </div>
                </div>
              </div>
            @endforeach
          </div>
        @else
          <div class="empty-state">
            <i class="fa-solid fa-inbox"></i>
            No orders yet. Start shopping!
          </div>
        @endif

      </div>

      {{-- ================= WISHLIST ================= --}}
      <div class="tab-pane fade" id="wishlist" role="tabpanel">

        <h1 class="section-title">
          <i class="fa-regular fa-heart me-2 text-primary"></i>My Wishlist
        </h1>

        @if(isset($wishlist) && count($wishlist) > 0)
          <div class="row g-3">
            @foreach($wishlist as $item)
              <div class="col-12 col-sm-6 col-lg-4">
                <div class="wish-card">
                  <div class="wish-name">{{ $item->name }}</div>
                  <div class="wish-price">₱{{ number_format($item->price, 2) }}</div>
                  <a href="{{ route('product_detail', $item->id) }}"
                     class="text-decoration-none">
                    <button class="wish-btn">
                      <i class="fa-regular fa-eye me-1"></i> View Item
                    </button>
                  </a>
                </div>
              </div>
            @endforeach
          </div>
        @else
          <div class="empty-state">
            <i class="fa-regular fa-heart"></i>
            Your wishlist is empty.
          </div>
        @endif

      </div>

      {{-- ================= SETTINGS ================= --}}
      <div class="tab-pane fade" id="settings" role="tabpanel">

        <h1 class="section-title">Account Settings</h1>

        <div class="d-flex flex-column gap-4">

          {{-- Personal Information --}}
          <div class="content-card">
            <div class="d-flex align-items-center justify-content-between mb-3">
              <div class="content-card-title">
                <i class="fa-solid fa-user text-primary"></i> Personal Information
              </div>
              <button class="edit-btn">
                <i class="fa-solid fa-pen"></i> Edit
              </button>
            </div>
            <div class="row g-2">
              <div class="col-6">
                <div class="info-tile">
                  <div class="label">Full Name</div>
                  <div class="value">{{ $user->first_name }} {{ $user->last_name }}</div>
                </div>
              </div>
              <div class="col-6">
                <div class="info-tile">
                  <div class="label">Email</div>
                  <div class="value">{{ $user->email }}</div>
                </div>
              </div>
              @if(isset($user->phone))
                <div class="col-6">
                  <div class="info-tile">
                    <div class="label">Phone</div>
                    <div class="value">{{ $user->phone }}</div>
                  </div>
                </div>
              @endif
              @if(isset($user->birthday))
                <div class="col-6">
                  <div class="info-tile">
                    <div class="label">Birthday</div>
                    <div class="value">
                      {{ \Carbon\Carbon::parse($user->birthday)->format('M d, Y') }}
                    </div>
                  </div>
                </div>
              @endif
            </div>
          </div>

          {{-- Security --}}
          <div class="content-card">
            <div class="content-card-title mb-3">🔒 Security</div>
            <div class="d-flex flex-column gap-2">
              <button class="sec-btn">
                Change Password
                <i class="fa-solid fa-chevron-right"></i>
              </button>
              <button class="sec-btn danger">
                Delete Account
                <i class="fa-solid fa-chevron-right"></i>
              </button>
            </div>
          </div>

        </div>
      </div>{{-- end settings --}}

    </div>{{-- end tab-content --}}
  </div>

</div>{{-- end row --}}

@endsection
